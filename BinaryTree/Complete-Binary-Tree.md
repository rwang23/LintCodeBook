##Complete Binary Tree

21% Accepted

	Check a binary tree is completed or not. A complete binary tree is not binary tree that every level is completed filled except the deepest level. In the deepest level, all nodes must be as left as possible. See more definition

	Have you met this question in a real interview? Yes
	Example
	    1
	   / \
	  2   3
	 /
	4
	is a complete binary.

	    1
	   / \
	  2   3
	   \
	    4
	is not a complete binary.

####Challenge
Do it in O(n) time

####Tags Expand
Binary Tree

###思路
- [Level Order Traversal](http://www.geeksforgeeks.org/check-if-a-given-binary-tree-is-complete-tree-or-not/)
- [Recursion](http://www.geeksforgeeks.org/check-whether-binary-tree-complete-not-set-2-recursive-solution/)
- 自己用的递归的方法,这个递归也是找规律,这道题递归不按套路出牌
- 先找出所有节点的数量
- 如果有一个点的index >= 所有节点数量了,说明肯定超出了,不是complete的,可以再看一下geeksforgeeks的递归思路

``` java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root, the root of binary tree.
     * @return true if it is a complete binary tree, or false.
     */
    int number = 0;
    public boolean isComplete(TreeNode root) {
        // Write your code here
        if (root == null) {
            return true;
        }
        number = count(root);
        return valid(root, 0);

    }

    public int count(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = count(root.left);
        int right = count(root.right);

        return left + right + 1;
    }

    public boolean valid(TreeNode root, int index) {
        if (root == null) {
            return true;
        }

        if (index >= number) {
            return false;
        }

        boolean left = valid(root.left, 2*index + 1);
        boolean right = valid(root.right, 2*index + 2);

        return left && right;
    }
}

```
