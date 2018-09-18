##Closest Binary Search Tree Value

	Total Accepted: 9613 Total Submissions: 28659 Difficulty: Easy
	Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

	Note:
	Given target value is a floating point.
	You are guaranteed to have only one unique value in the BST that is closest to the target.

####思路
- 分治(因为是BST所以每次保留一边就行)
- O(logn)
- BST不用一来就准备利用中序遍历，也可以根据二分呀，每次舍弃一半子树，会更快

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
     * @param root: the given BST
     * @param target: the given target
     * @return: the value in the BST that is closest to the target
     */
    double min = Double.MAX_VALUE; 
    int find = 0;
    
    
    public int closestValue(TreeNode root, double target) {
        // write your code here
        if (root == null) {
            return 0;
        }
        
        TreeNode cur = root;
        while (cur != null) {
            if (Math.abs(cur.val - target) < min) {
                min = Math.abs(cur.val - target);
                find = cur.val;
            }
            
            if (target - cur.val == 0.0) {
                return cur.val;
            } else if (target - cur.val > 0.0) {
                cur = cur.right;
            } else {
                cur = cur.left;
            }
        }
        
        return find;
    }
}
```

