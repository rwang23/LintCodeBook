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

----
####非递归
```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST (TreeNode root){
           Stack<TreeNode> stack = new Stack<TreeNode> ();
           TreeNode cur = root ;
           TreeNode pre = null ;
           while (!stack.isEmpty() || cur != null) {
               if (cur != null) {
                   stack.push(cur);
                   cur = cur.left ;
               } else {
                   TreeNode p = stack.pop() ;
                   if (pre != null && p.val <= pre.val) {
                       return false ;
                   }
                   pre = p ;
                   cur = p.right ;
               }
           }
           return true ;
       }
}

```

-----
####递归
```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: True if the binary tree is BST, or false
     */
    public boolean isValidBST(TreeNode root) {
    return isValidBST(root, Double.NEGATIVE_INFINITY, Double.POSITIVE_INFINITY);
}

    public boolean isValidBST(TreeNode p, double min, double max){
        if(p==null)
            return true;

        if(p.val <= min || p.val >= max)
            return false;

        return isValidBST(p.left, min, p.val) && isValidBST(p.right, p.val, max);
    }
}
```
