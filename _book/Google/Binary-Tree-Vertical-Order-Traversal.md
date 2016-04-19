##Binary Tree Vertical Order Traversal

    Total Accepted: 4483 Total Submissions: 14861 Difficulty: Medium
    Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

    If two nodes are in the same row and column, the order should be from left to right.

    Examples:
    Given binary tree [3,9,20,null,null,15,7],
        3
       / \
      9  20
        /  \
       15   7
    return its vertical order traversal as:
    [
      [9],
      [3,15],
      [20],
      [7]
    ]
    Given binary tree [3,9,20,4,5,2,7],
        _3_
       /   \
      9    20
     / \   / \
    4   5 2   7
    return its vertical order traversal as:
    [
      [4],
      [9],
      [3,5,2],
      [20],
      [7]
    ]

####思路
- 记录下每个节点的左右distance, root是0,它的左子点是-1,右子点是1
- 使用Map<Integer, List<Integer>>, key是distance,value就是对应distance的节点的value
- 因为需要从上到下,从左到右的顺序,那么就只能level order遍历
- 如果只需要从左到右,那就只需要preorder遍历
- 因为在遍历过程中需要读取queue poll出来节点的distance,所以要么做一个pair类来存distance,或者再来一个hashmap

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

    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null) {
            return result;
        }

        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
        Map<TreeNode, Integer> distanceMap = new HashMap<TreeNode, Integer>();
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        int maxDistance = 0;
        int minDistance = 0;

        queue.offer(root);
        distanceMap.put(root, 0);

        while (!queue.isEmpty()) {
            TreeNode cur = queue.poll();
            int distance = distanceMap.get(cur);
            maxDistance = (distance > maxDistance) ? distance : maxDistance;
            minDistance = (distance < minDistance) ? distance : minDistance;

            if (map.containsKey(distance)) {
                map.get(distance).add(cur.val);
            } else {
                List<Integer> list = new ArrayList<Integer>();
                list.add(cur.val);
                map.put(distance, list);
            }

            if (cur.left != null) {
                queue.offer(cur.left);
                distanceMap.put(cur.left, distance - 1);
            }
            if (cur.right != null) {
                queue.offer(cur.right);
                distanceMap.put(cur.right, distance + 1);
            }
        }

        for (int i = minDistance; i <= maxDistance; i++) {
            result.add(map.get(i));
        }

        return result;
    }
}
```
