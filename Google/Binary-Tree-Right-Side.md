##Binary Tree Right Side

	Total Accepted: 36196 Total Submissions: 108461 Difficulty: Medium
	Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

	For example:
	Given the following binary tree,
	   1            <---
	 /   \
	2     3         <---
	 \     \
	  5     4       <---
	You should return [1, 3, 4].

####思路
- level order

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();

        if (root == null) {
            return result;
        }

        TreeNode cur = root;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(cur);

        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                cur = queue.poll();
                if (cur.left != null) {
                    queue.offer(cur.left);
                }
                if (cur.right != null) {
                    queue.offer(cur.right);
                }
            }
            result.add(cur.val);
        }

        return result;
    }
}
```
