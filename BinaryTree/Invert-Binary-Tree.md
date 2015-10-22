##Invert Binary Tree

40% Accepted

	Invert a binary tree.

	Have you met this question in a real interview? Yes
	Example
	  1         1
	 / \       / \
	2   3  => 3   2
	   /       \
	  4         4

####Challenge
- Do it in recursion is acceptable, can you do it without recursion?

####Tags Expand
- Binary Tree

----
####递归解法
- 分治分别翻转左右子树

```java
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        // write your code here
        if (root == null) {
            return;
        }

        invertBinaryTree(root.left);
        invertBinaryTree(root.right);

        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
    }
}

```

----
####非递归
- 遍历 互相交换左右子树

```java
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        // write your code here
        if (root == null) {
            return;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();

        TreeNode cur = root;
        queue.offer(cur);
        while (!queue.isEmpty()) {

            TreeNode top = queue.peek();
            queue.poll();
            TreeNode temp = top.left;
            top.left = top.right;
            top.right = temp;
            if (top.left != null) {
                queue.offer(top.left);
            }
            if (top.right != null) {
                queue.offer(top.right);
            }
        }
    }
}
```


