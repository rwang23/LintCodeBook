##House Robber III

	Total Accepted: 5903 Total Submissions: 16011 Difficulty: Medium
	The thief has found himself a new place for his thievery again.
	 There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house.
	 After a tour, the smart thief realized that "all houses in this place forms a binary tree".
	 It will automatically contact the police if two directly-linked houses were broken into on the same night.

	Determine the maximum amount of money the thief can rob tonight without alerting the police.

	Example 1:
	     3
	    / \
	   2   3
	    \   \
	     3   1
	Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
	Example 2:
	     3
	    / \
	   4   5
	  / \   \
	 1   3   1
	Maximum amount of money the thief can rob = 4 + 5 = 9.

####思路
- 二叉树一来就想到了递归规律
- 分别找左子树,右子树,以及左子树的左右,右子树的左右sum
- leetcode跑出来600ms,有点长,然后想到了记忆化
- 然后用hashmap来做记忆化优化就可以了
- 记忆化后跑出来 8ms

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
    Map<TreeNode, Integer> = new HashMap<TreeNode, Integer>();
    public int rob(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int leftChild = 0;
        int rightChild = 0;
        int leftGrandChild = 0;
        int rightGrandChild = 0;

        if (root.left != null) {
            leftChild = rob(root.left);
            leftGrandChild = rob(root.left.left) + rob(root.left.right);
        }
        if (root.right != null) {
            rightChild = rob(root.right);
            rightGrandChild = rob(root.right.left) + rob(root.right.right);
        }

        return Math.max(leftGrandChild + rightGrandChild + root.val, leftChild + rightChild);

    }
}
```

####优化
- 使用hashmap来做记忆化搜索

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
    Map<TreeNode, Integer> map = new HashMap<TreeNode, Integer>();

    public int rob(TreeNode root) {
        if (root == null) {
            return 0;
        }

        if (map.containsKey(root)) {
            return map.get(root);
        }

        int leftChild = 0;
        int rightChild = 0;
        int leftGrandChild = 0;
        int rightGrandChild = 0;

        if (root.left != null) {
            leftChild = rob(root.left);
            leftGrandChild = rob(root.left.left) + rob(root.left.right);
        }
        if (root.right != null) {
            rightChild = rob(root.right);
            rightGrandChild = rob(root.right.left) + rob(root.right.right);
        }

        int sum = Math.max(leftGrandChild + rightGrandChild + root.val, leftChild + rightChild);
        map.put(root, sum);
        return sum;

    }
}
```
