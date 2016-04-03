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
- 还有解释注意 二叉树的 DFS 跟其他的通常有点不一样,
- 其他DFS 一般在list里边加入了一个数,后来回溯的时候会再删除掉
- 然后二叉树DFS一般不用回溯,所以不用删除,这样导致传递的arraylist其实指向的是一个
- 所以每次递归中要声明一个新的arraylist,这样才不会错误

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

        List<Integer> path = new ArrayList<Integer>();
        dfs(result, path, root, sum);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> path, TreeNode root, int sum) {
        if (root == null) {
            return;
        }

        List<Integer> newPath = new ArrayList<Integer>(path);
        sum = sum - root.val;
        newPath.add(root.val);
        if (root.left == null && root.right == null && sum == 0) {
            result.add(new ArrayList<Integer>(newPath));
            return;
        }

        dfs(result, newPath, root.left, sum);
        dfs(result, newPath, root.right, sum);


    }
}
```
