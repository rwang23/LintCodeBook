##Largest BST Subtree
	Total Accepted: 3112 Total Submissions: 11754 Difficulty: Medium
	Given a binary tree, find the largest subtree which is a Binary Search Tree (BST), where largest means subtree with largest number of nodes in it.

	Note:
	A subtree must include all of its descendants.
	Here's an example:
	    10
	    / \
	   5  15
	  / \   \
	 1   8   7
	The Largest BST Subtree in this case is the highlighted one.
	The return value is the subtree's size, which is 3.
	Hint:

	You can recursively use algorithm similar to 98. Validate Binary Search Tree at each node of the tree, which will result in O(nlogn) time complexity.
	Follow up:
	Can you figure out ways to solve it with O(n) time complexity?

####思路
- 这道题可以直接写一个判断isValid的函数,然后遍历整个BST,对每个节点进行判断
- 这样很简单 时间复杂度O(nlogn)
- 不过我以来就想的是从bottom -> top的递归,这样只需要遍历一遍整个BST就能判断出来了
- 为了直接判断,就保存了如果作为合格的BST,每个节点所应有的最大值和最小值
- 如果不合格就将整个结点以及这个结点父亲都置为不合格,结果保存在一个全局变量maxBST里边

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private class Element {
        private int max;
        private int min;
        private int count;
        Element(int max, int min, int count) {
            this.max = max;
            this.min = min;
            this.count = count;
        }
    }

    int maxBST = 1;
    public int largestBSTSubtree(TreeNode root) {
        if (root == null) {
            return 0;
        }
        helper(root);
        return maxBST;
    }

    public Element helper(TreeNode root) {
        if (root == null) {
            return null;
        }

        if (root.left == null && root.right == null) {
            return new Element(root.val, root.val, 1);
        }

        Element left = helper(root.left);
        Element right = helper(root.right);

        if (root.left != null) {
            if (left.max > root.val || root.left.val > root.val || left.count == 0) {
                return new Element(0, 0, 0);
            }
        } else {
            left = new Element(Integer.MIN_VALUE, Integer.MAX_VALUE, 0);
        }

        if (root.right != null) {
            if (right.min < root.val || root.right.val < root.val || right.count == 0) {
                return new Element(0, 0, 0);
            }
        } else {
            right = new Element(Integer.MIN_VALUE, Integer.MAX_VALUE, 0);
        }

        maxBST = Math.max(maxBST, right.count + left.count + 1);
        return new Element(Math.max(right.max, root.val), Math.min(left.min, root.val), right.count + left.count + 1);

    }
}
```
