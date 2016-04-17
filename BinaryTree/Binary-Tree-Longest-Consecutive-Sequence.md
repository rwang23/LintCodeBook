##Binary Tree Longest Consecutive Sequence

    Total Accepted: 7180 Total Submissions: 19552 Difficulty: Medium
    Given a binary tree, find the length of the longest consecutive sequence path.

    The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

    For example,
       1
        \
         3
        / \
       2   4
            \
             5
    Longest consecutive sequence path is 3-4-5, so return 3.
       2
        \
         3
        /
       2
      /
     1
    Longest consecutive sequence path is 2-3,not3-2-1, so return 2.

####思路
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
    int max = 0;
    public int longestConsecutive(TreeNode root) {
        helper(root);
        return max;
    }

    public int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = 1;
        int right = 1;
        if (root.left != null && root.val + 1 == root.left.val) {
            left = helper(root.left) + 1;
        } else {
            helper(root.left);
        }
        if (root.right != null && root.val + 1 == root.right.val) {
            right = helper(root.right) + 1;
        } else {
            helper(root.right);
        }
        max = Math.max(max, Math.max(left, right));

        return Math.max(left, right);

    }
}
```

####后来写的

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
    int maxLen = 1;
    public int longestConsecutive(TreeNode root) {
        if (root == null) {
            return 0;
        }
        longestConsecutive(root, 1);
        return maxLen;
    }

    public void longestConsecutive(TreeNode root, int len) {
        if (root == null) {
            return;
        }

        if (root.left != null) {
            if (root.left.val == root.val + 1) {
                longestConsecutive(root.left, len + 1);
                maxLen = Math.max(maxLen, len + 1);
            } else {
                longestConsecutive(root.left, 1);
            }
        }

        if (root.right != null) {
            if (root.right.val == root.val + 1) {
                longestConsecutive(root.right, len + 1);
                maxLen = Math.max(maxLen, len + 1);
            } else {
                longestConsecutive(root.right, 1);
            }
        }
    }
}
```
