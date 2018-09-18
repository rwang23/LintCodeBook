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
     * @param root: the root of the binary tree
     * @return: all root-to-leaf paths
     */
    public List<String> binaryTreePaths(TreeNode root) {
        // write your code here
        List<String> results = new ArrayList<String>(0);
        if (root == null) {
            return results;
        }
        StringBuilder sb = new StringBuilder();
        divide(root, sb, results);
        
        return results;
        
    }
    
    public void divide(TreeNode root, StringBuilder sb, List<String> results) {
        
        if (root.left == null && root.right == null) {
            sb.append(root.val);
            String result = new String(sb.toString());
            results.add(result);
            return;
        }
        
        sb.append(root.val);
        sb.append("->");
        if (root.left != null) {
            StringBuilder sbLeft = new StringBuilder(sb);
             divide(root.left, sbLeft, results);
        }
        
        if (root.right != null) {
            StringBuilder sbRight = new StringBuilder(sb);
            divide(root.right, sbRight, results);
        }
    }
}
```
