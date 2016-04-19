##Closest Binary Search Tree Value

	Total Accepted: 9613 Total Submissions: 28659 Difficulty: Easy
	Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

	Note:
	Given target value is a floating point.
	You are guaranteed to have only one unique value in the BST that is closest to the target.

####思路
- 分治(因为是BST所以每次保留一边就行)
- O(logn)

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
    int close = Integer.MAX_VALUE;
    double min = Double.MAX_VALUE;
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return -1;
        }

        if (Math.abs((double)(root.val) - target) < min) {
            min = Math.abs((double)(root.val) - target);
            close = root.val;
        }

        if ((double)(root.val) - target >= 0.0) {
            closestValue(root.left, target);
        } else {
            closestValue(root.right, target);
        }

        return close;

    }
}
```

####非递归
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
    public int closestValue(TreeNode root, double target) {
        if (root == null) {
            return -1;
        }

        double diff = Math.abs((double)root.val - target);
        double minDiff = diff;
        int res = root.val;
        while (root != null) {
            if (target == (double)root.val) {
                return root.val;
            } else if (target > (double)root.val) {
                root = root.right;
            } else {
                root = root.left;
            }
            if (root != null) {
                diff = Math.abs((double)root.val - target);
                minDiff = Math.min(diff, minDiff);
                if (diff == minDiff) {
                    res = root.val;
                }
            }
        }
        return res;
    }
}
```

