##Path Sum II
	Total Accepted: 75122 Total Submissions: 268818 Difficulty: Medium
	Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

	For example:
	Given the below binary tree and sum = 22,
	              5
	             / \
	            4   8
	           /   / \
	          11  13  4
	         /  \    / \
	        7    2  5   1
	return
	[
	   [5,4,11,2],
	   [5,8,4,5]
	]

####思路
- 注意,一定是从root到节点
- 理解题意错了,十分钟的题花了三十分钟debug,后来才明白理解错了


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
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null) {
            return result;
        }
        List<Integer> list = new ArrayList<Integer>();
        list.add(root.val);
        dfs(root, sum - root.val, result, list);
        return result;
    }

    public void dfs(TreeNode root, int sum, List<List<Integer>> result, List<Integer> list) {
        if (sum == 0 && root.left == null && root.right == null) {
            result.add(new ArrayList<Integer>(list));
            return;
        }
        if (root == null) {
            return;
        }

        if (root.left != null) {
            list.add(root.left.val);
            dfs(root.left, sum - root.left.val, result, list);
            list.remove(list.size() - 1);

        }
        if (root.right != null) {
            list.add(root.right.val);
            dfs(root.right, sum - root.right.val, result, list);
            list.remove(list.size() - 1);
        }
    }
}
```
