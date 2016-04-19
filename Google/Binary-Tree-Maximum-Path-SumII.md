##Binary Tree Maximum Path Sum II

41% Accepted

	Given a binary tree, find the maximum path sum from root.

	The path may end at any node in the tree.

	Have you met this question in a real interview? Yes
	Example
	Given the below binary tree:

	  1
	 / \
	2   3
	return 4. (1->3)

####Tags Expand
- Binary Tree



```java
public class Solution {
    /**
     * @param root the root of binary tree.
     * @return an integer
     */
    public int maxPathSum2(TreeNode root) {
        // Write your code here
        if (root == null) {
            return 0;
        }

        int left = maxPathSum2(root.left);
        int right = maxPathSum2(root.right);

        return Math.max(left, right) + root.val;
    }
}

```
