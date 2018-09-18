##Balanced Binary Tree

40% Accepted

	Given a binary tree, determine if it is height-balanced.

	For this problem, a height-balanced binary tree is defined as a binary tree
    in which the depth of the two subtrees of every node never differ by more than 1.

	Have you met this question in a real interview? Yes
	Example
	Given binary tree A={3,9,20,#,#,15,7}, B={3,#,20,15,7}

	A)  3            B)    3
	   / \                  \
	  9  20                 20
	    /  \                / \
	   15   7              15  7
	The binary tree A is a height-balanced binary tree, but B is not.

####Tags Expand
- Binary Search
- Divide and Conquer
- Recursion

####思路


####我的代码

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
     * @param root: The root of binary tree.
     * @return: True if this Binary tree is Balanced, or false.
     */
    public boolean balanced = true; 
    
    public boolean isBalanced(TreeNode root) {
        // write your code here
        if (root == null) {
            return true;
        }
        
        getHeight(root);
        
        return balanced;
    }
    
    public int getHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = getHeight(root.left);
        int right = getHeight(root.right);
        if (Math.abs(left - right) > 1) {
            balanced = false;
        }
        
        return Math.max(left, right) + 1;
    }
}
```
