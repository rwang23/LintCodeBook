##Binary Tree Paths


	Given a binary tree, return all root-to-leaf paths.

	Have you met this question in a real interview? Yes
	Example
	Given the following binary tree:

	   1
	 /   \
	2     3
	 \
	  5
	All root-to-leaf paths are:

	[
	  "1->2->5",
	  "1->3"
	]

####Tags Expand
Binary Tree Binary Tree Traversal Facebook Google

####思路
- 唯一需要注意的是,每进入新一层,就要重新生命string,不然有可能会改变string值,导致错误

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
    public List<String> binaryTreePaths(TreeNode root) {
        if (root == null) {
            return new ArrayList<String>();
        }

        List<String> result = new ArrayList<String>();
        StringBuilder string = new StringBuilder();
        dfs(root, result, string);
        return result;
    }

    public void dfs(TreeNode root, List<String> result, StringBuilder string) {
        if (root == null) {
            return;
        }
        string = new StringBuilder(string);
        if (root.left == null && root.right == null) {
            string.append(root.val);
            result.add(new String(string.toString()));
            return;
        }

        string.append(root.val);
        string.append("->");
        dfs(root.left, result, string);
        dfs(root.right, result, string);
    }
}
```
