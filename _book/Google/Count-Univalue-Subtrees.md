##Count Univalue Subtrees

	Total Accepted: 4816 Total Submissions: 13508 Difficulty: Medium
	Given a binary tree, count the number of uni-value subtrees.

	A Uni-value subtree means all nodes of the subtree have the same value.

	For example:
	Given binary tree,
	              5
	             / \
	            1   5
	           / \   \
	          5   5   5
	return 4.

####思路
- 稍微跟直接的分治法有点区别,
- 直接想分治法,从子树出发,发现返回int不管用,这样做比如要两轮递归
- 所以思考到先判断是否是unival subtree,再计算数量,
- 用一个global int值来记录数量就行了

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
    int count = 0;
    public int countUnivalSubtrees(TreeNode root) {
        isUnivalSubtree(root);
        return count;
    }

    public boolean isUnivalSubtree(TreeNode root) {
        if (root == null) {
            return true;
        }

        boolean left = isUnivalSubtree(root.left);
        boolean right = isUnivalSubtree(root.right);
        boolean head;

        if (root.left != null && root.right != null) {
            head = (root.val == root.left.val && root.val == root.right.val);
        } else if (root.left != null && root.right == null) {
            head = (root.val == root.left.val);
        } else if (root.left == null && root.right != null) {
            head = (root.val == root.right.val);
        } else {
            head = true;
        }

        if (left && right && head) {
            count++;
        }

        return left && right && head;
    }
}
```
