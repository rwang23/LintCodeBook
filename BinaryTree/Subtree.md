##Subtree

20% Accepted

	You have two every large binary trees: T1, with millions of nodes, and T2, with hundreds of nodes. Create an algorithm to decide if T2 is a subtree of T1.

	Have you met this question in a real interview? Yes
	Example
	T2 is a subtree of T1 in the following case:

	       1                3
	      / \              /
	T1 = 2   3      T2 =  4
	        /
	       4
	T2 isn't a subtree of T1 in the following case:

	       1               3
	      / \               \
	T1 = 2   3       T2 =    4
	        /
	       4
	Note
	A tree T2 is a subtree of T1 if there exists a node n in T1 such that the subtree of n is identical to T2. That is, if you cut off the tree at node n, the two trees would be identical.

####Tags Expand
- Recursion
- Binary Tree

####思路


```java
public class Solution {
    /**
     * @param T1, T2: The roots of binary tree.
     * @return: True if T2 is a subtree of T1, or false.
     */
    public boolean isSubtree(TreeNode T1, TreeNode T2) {
        // write your code here
        if (T2 == T1 ){
            return true;
        }else if (T1 == null) {
            return false;
        }else {
            return isSubtree(T1.left, T2) || isSubtree(T1.right, T2) || isSameTree(T1, T2);
        }

    }

    public boolean isSameTree(TreeNode T1, TreeNode T2) {
        if(T1 == null && T2 == null)
            return true;
        if(T1 == null || T2 == null)
            return false;
        if(T1.val != T2.val)
            return false;
        return isSameTree(T1.left,T2.left) && isSameTree(T1.right, T2.right);
    }
}

```
