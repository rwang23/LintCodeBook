##Kth Smallest Element in a BST

	Total Accepted: 37687 Total Submissions: 103867 Difficulty: Medium
	Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

	Note:
	You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

	Follow up:
	What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

####思路
- in order遍历
- O(k)

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
    public int kthSmallest(TreeNode root, int k) {
        if (root == null) {
            throw new IllegalArgumentException("Please use an valid root");
        }

        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode cur = root;
        int count = 0;

        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.pop();
            if (++count == k) {
                return cur.val;
            }
            cur = cur.right;
        }

        return -1;
    }
}
```

####Follow Up
If we could add a count field in the BST node class, it will take O(n) time when we calculate the count value for the whole tree, but after that, it will take O(logn) time when insert/delete a node or calculate the kth smallest element.

- [source1](https://leetcode.com/discuss/43464/what-if-you-could-modify-the-bst-nodes-structure)
- [source2](http://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)
