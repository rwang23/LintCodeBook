##Binary Tree Path Sum
	Given a binary tree,
	find all paths that sum of the nodes in the path equals to a given number target.

	A valid path is from root node to any of the leaf nodes.

	 Binary Tree Path Sum Show result

	Given a binary tree, find all paths that sum of the nodes in the path equals to a given number target.

	A valid path is from root node to any of the leaf nodes.

	Have you met this question in a real interview? Yes
	Example
	Given a binary tree, and target = 5:

	     1
	    / \
	   2   4
	  / \
	 2   3
	return

	[
	  [1, 2, 2],
	  [1, 4]
	]

####思路
- 本来我的代码很简洁,递归到下一层null的时候去判断是否加入
- 但是这样就很容易出错
- 还是常规做法,判断left是否存在,right是否存在

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
     * @param root the root of binary tree
     * @param target an integer
     * @return all valid paths
     */
    public List<List<Integer>> result = new ArrayList<List<Integer>>();

    public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
        // Write your code here
        if (root == null) {
            return new ArrayList<List<Integer>>();
        }
        List<Integer> list = new ArrayList<Integer>();
        list.add(root.val);
        helper(root, target - root.val, list);
        return result;
    }
    public void helper(TreeNode root, int target, List<Integer> list ) {
        if (target == 0) {
            result.add(new ArrayList<Integer>(list));
            return;
        }
        if (root == null) {
            return;
        }

        if (root.left != null) {
            list.add(root.left.val);
            helper(root.left, target - root.left.val, list);
            list.remove(list.size() - 1);
        }
        if (root.right != null) {
            list.add(root.right.val);
            helper(root.right, target - root.right.val, list);
            list.remove(list.size() - 1);
        }
    }
}
```
