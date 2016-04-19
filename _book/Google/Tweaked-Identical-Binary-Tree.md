##Tweaked Identical Binary Tree

	Check two given binary trees are identical or not.
	Assuming any number of tweaks are allowed. A tweak is defined as a swap of the children of one node in the tree.

	Example
	    1             1
	   / \           / \
	  2   3   and   3   2
	 /                   \
	4                     4
	are identical.

	    1             1
	   / \           / \
	  2   3   and   3   2
	 /             /
	4             4
	are not identical.

	Note
	There is no two nodes with the same value in the tree.

	Challenge
	O(n) time


####思路
- 主要是理解题意,理解错了就错
- 任意节点可以交换
- 看似很难,其实不难

```java
public class Solution {
    /**
     * @param a, b, the root of binary trees.
     * @return true if they are tweaked identical, or false.
     */
    public boolean isTweakedIdentical(TreeNode a, TreeNode b) {
        if (a == null && b == null) {
            return true;
        }
        if (a == null || b == null) {
            return false;
        }
        if (a.val != b.val) {
            return false;
        }

        if (isTweakedIdentical(a.left, b.left) && isTweakedIdentical(a.right, b.right)) {
            return true;
        }

        if (isTweakedIdentical(a.left, b.right) && isTweakedIdentical(a.right, b.left)) {
            return true;
        }

        return false;
    }
}
```
