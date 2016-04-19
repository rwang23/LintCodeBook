##Maximum Depth of Binary Tree

55% Accepted

	Given a binary tree, find its maximum depth.

	The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

	Have you met this question in a real interview? Yes
	Example
	Given a binary tree as follow:

	  1
	 / \
	2   3
	   / \
	  4   5
	The maximum depth is 3.

####Tags Expand
- Divide and Conquer
- Recursion
- Binary Tree

####思路
- 简化成两件事情：求左边的最大 和 求右边的最大； 最后合并

```java
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

###非递归
- 就是level order traversal

```java
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();

        TreeNode cur = root;
        queue.offer(root);
        int depth = 0;

        while(queue.peek() != null){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                cur = queue.peek();
                if(cur.left != null){
                    queue.offer(cur.left);
                }
                if(cur.right != null){
                    queue.offer(cur.right);
                }
                queue.poll();
            }
            depth++;

        }
        return depth;
    }
}
```
