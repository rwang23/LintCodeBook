##Binary Tree Zigzag Level Order Traversal
	Total Accepted: 56958 Total Submissions: 201334 Difficulty: Medium
	Given a binary tree, return the zigzag level order traversal of its nodes' values.
	(ie, from left to right, then right to left for the next level and alternate between).

	For example:
	Given binary tree {3,9,20,#,#,15,7},
	    3
	   / \
	  9  20
	    /  \
	   15   7
	return its zigzag level order traversal as:
	[
	  [3],
	  [20,9],
	  [15,7]
	]

####思路
- 使用deque,这样就能两边都能出能进啦

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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null) {
            return result;
        }

        Deque<TreeNode> queue = new LinkedList<TreeNode>();
        TreeNode cur = root;
        queue.offerFirst(cur);
        boolean flag = true;

        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<Integer>();
            for (int i = 0; i < size; i++) {
                if (flag) {
                    cur = queue.pollFirst();
                    list.add(cur.val);

                    if (cur.left != null) {
                        queue.offerLast(cur.left);
                    }

                    if (cur.right != null) {
                        queue.offerLast(cur.right);
                    }
                } else {
                    cur = queue.pollLast();
                    list.add(cur.val);

                    if (cur.right != null) {
                        queue.offerFirst(cur.right);
                    }

                    if (cur.left != null) {
                        queue.offerFirst(cur.left);
                    }
                }

            }
            flag = !flag;
            result.add(list);
        }
        return result;
    }
}
```
