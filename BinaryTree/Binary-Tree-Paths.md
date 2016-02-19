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
     * @param root the root of the binary tree
     * @return all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        // Write your code here
        if (root == null) {
            return new ArrayList<String>();
        }

        List<String> result = new ArrayList<String>();
        StringBuilder string = new StringBuilder("");
        helper(root, result, string);
        return result;
    }

    public void helper(TreeNode root, List<String> result, StringBuilder string) {
        if (root.left == null && root.right == null) {
            string.append(Integer.toString(root.val));
            result.add(new String(string.toString()));
            return;
        }

        string.append(Integer.toString(root.val));
        string.append("->");

        if (root.left != null) {
            helper(root.left, result, new StringBuilder(string) );
        }
        if (root.right != null) {
            helper(root.right, result, new StringBuilder(string));
        }
    }
}
```
