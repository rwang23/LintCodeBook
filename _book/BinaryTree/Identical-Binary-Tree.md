##Identical Binary Tree

39% Accepted

	Check if two binary trees are identical.
	Identical means the two binary trees have the same structure and every identical position has the same value.

	Have you met this question in a real interview? Yes
	Example
	    1             1
	   / \           / \
	  2   2   and   2   2
	 /             /
	4             4
	are identical.

	    1             1
	   / \           / \
	  2   3   and   2   3
	 /               \
	4                 4
	are not identical.

####Tags Expand
Binary Tree

####思路

```java
public class Solution {
    /**
     * @param a, b, the root of binary trees.
     * @return true if they are identical, or false.
     */
    public boolean isIdentical(TreeNode a, TreeNode b) {
        // Write your code here
        /*
        这个 if else if用得不错,else中已经排除a==null b==null这种情况,很简单就写出来了
         */
        if (a == null && b == null) {
            return true;
        } else if (a == null || b == null) {
            return false;
        }
        return a.val == b.val ? isIdentical(a.left, b.left) && isIdentical(a.right, b.right) : false;
    }
}
```
