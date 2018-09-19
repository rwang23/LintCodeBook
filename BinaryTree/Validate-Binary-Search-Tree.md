##Validate Binary Search Tree

22% Accepted

	Given a binary tree, determine if it is a valid binary search tree (BST).

	Assume a BST is defined as follows:

	The left subtree of a node contains only nodes with keys less than the node's key.

	The right subtree of a node contains only nodes with keys greater than the node's key.

	Both the left and right subtrees must also be binary search trees.

	Have you met this question in a real interview? Yes
	Example
	An example:

	  2
	 / \
	1   3
	   /
	  4
	   \
	    5
	The above binary tree is serialized as {2,1,3,#,#,4,#,#,5} (in level order).

####Tags Expand
- Divide and Conquer
- Recursion
- Binary Search Tree
- Binary Tree

####思路
- 非递归思路无非就是一个中序遍历，如果不满足前值小于后值，则不是BST
- 递归思路:新建一个函数，把当前结点所能拥有的最大值与最小值传入，如果此节点超过最大值或者小于最小值，说明不符合要求
- 因为test case含有Integer.MAX_VALUE 和 Integer.MIN_VALUE, 所以判断的时候用的Double.NEGATIVE_INFINITY, Double.POSITIVE_INFINITY

----
####非递归
```java
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
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        // write your code here
        if (root == null) {
            return true;
        }
        
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode cur = root;
        
        double pre = Double.NEGATIVE_INFINITY;
        while (!stack.isEmpty() || cur != null) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }
            
            cur = stack.pop();
            if (cur.val <= pre) {
                return false;
            }
            pre = cur.val;
            cur = cur.right;
            
        }
        
        return true;
    }
}

```

-----
####递归
- 在函数里添加min, max或者做一个新的result type都可以
- 把父节点的值向下传，每次在递归的时候，就要保证在左子树的时候，此时的root的值不能比max大，右子树时，不能比min小
- 在上层已经限定好了值

```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Double.NEGATIVE_INFINITY, Double.POSITIVE_INFINITY);
    }

    public boolean isValidBST(TreeNode root, double min, double max){
        if (root == null) {
            return true;
        }

        if (root.val <= min || root.val >= max) {
            return false;
         }
         
        boolean left = isValidBST(root.left, min, root.val);
        boolean right = isValidBST(root.right, root.val, max);

        return left && right;
    }
}
```
