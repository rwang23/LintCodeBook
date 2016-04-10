##Closest Binary Search Tree Value II

	Total Accepted: 5710 Total Submissions: 17392 Difficulty: Hard
	Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

	Note:
	Given target value is a floating point.
	You may assume k is always valid, that is: k ≤ total nodes.
	You are guaranteed to have only one unique set of k values in the BST that are closest to the target.
	Follow up:
	Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?

	Hint:

	Consider implement these two helper functions:
	getPredecessor(N), which returns the next smaller node to N.
	getSuccessor(N), which returns the next larger node to N.
	Try to assume that each node has a parent pointer, it makes the problem much easier.
	Without parent pointer we just need to keep track of the path from the root to the current node using a stack.
	You would need two stacks to track the path in finding predecessor and successor node separately.

####思路
- 先inorder遍历BST
- 再用两个同向指针找到K个数

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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        List<Integer> result = new ArrayList<Integer>();
        if (root == null) {
            return result;
        }
        List<Integer> traverse = new ArrayList<Integer>();
        inorderTraverse(root, traverse);

        int size = traverse.size();
        for (int i = 0; i < k; i++) {
            result.add(traverse.get(i));
        }

        for (int i = k; i < size; i++) {
            int first = result.get(0);
            int cur = traverse.get(i);
            if (Math.abs((double)cur - target) < Math.abs((double)first - target)) {
                result.remove(0);
                result.add(cur);
            } else {
                break;
            }
        }
        return result;
    }

    public void inorderTraverse(TreeNode root, List<Integer> traverse) {
        if (root == null) {
            return;
        }
        inorderTraverse(root.left, traverse);
        traverse.add(root.val);
        inorderTraverse(root.right, traverse);

    }
}
```

####Follow Up
[Follow Up](https://leetcode.com/discuss/71820/java-5ms-iterative-following-hint-o-klogn-time-and-space)
- 最开始还不明白,然后把Balance BST 的图画出来就明白了
- 简直精妙
- 找predeccusor 和 successor
