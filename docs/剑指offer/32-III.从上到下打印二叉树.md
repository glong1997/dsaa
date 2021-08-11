### 剑指 Offer 32 - III. 从上到下打印二叉树 III

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

**提示：**

1. `节点总数 <= 1000`

题解：

>LinkedList的addLast和addFirst
>
>```
>if((res.size() & 1) == 0) tmp.addLast(node.val); // 偶数层 -> 队列头部
>else tmp.addFirst(node.val); // 奇数层 -> 队列尾部
>```
>
>

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null) return new ArrayList<>(){};
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        queue.add(root);	// 根结点进入队列
        while(!queue.isEmpty()) {
          	int n = queue.size();
            LinkedList<Integer> tmp = new LinkedList<>();
            for(int i = 0; i < n; i++) {
                TreeNode node = queue.poll();
                if((res.size() & 1) == 0) tmp.addLast(node.val); // 偶数层 -> 队列头部
                else tmp.addFirst(node.val); // 奇数层 -> 队列尾部
                if(node.left != null) queue.add(node.left);
                if(node.right != null) queue.add(node.right);
            }
            res.add(tmp);
        }
        return res;
    }
}
```

