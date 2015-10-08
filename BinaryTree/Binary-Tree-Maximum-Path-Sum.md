##Binary Tree Maximum Path Sum


23% Accepted

	Given a binary tree, find the maximum path sum.

	The path may start and end at any node in the tree.

	Have you met this question in a real interview? Yes
	Example
	Given the below binary tree:

	  1
	 / \
	2   3
	return 6.

####Tags Expand
- Divide and Conquer
- Dynamic Programming
- Recursion

####思路
- 任意节点到任意节点
- 有可能不经过根节点，也有可能经过根节点，所以求其中最大值
- 分治的方法，分别求左边最大，右边最大， 再比较 左最大+右最大+根节点 是不是会刷新最大值，如果不能的话还是去原来的最大值
- max为全局变量
- 最终maxPathSum返回的是max，而helper只是在求每一条边上的最大值
- 解法来源Leecode

```java
public class Solution {
    int max = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        helper(root);
        return max;
    }

    // helper returns the max branch
    // plus current node's value
    int helper(TreeNode root) {
        if (root == null) return 0;

        int left = Math.max(helper(root.left), 0);
        int right = Math.max(helper(root.right), 0);

        max = Math.max(max, root.val + left + right);

        return root.val + Math.max(left, right);
    }
}
```
