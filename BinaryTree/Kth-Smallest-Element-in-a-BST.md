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

####另一个O(n)的思路
- 算法思想类似于 Quick Select。
- 分别算出每个节点的子节点总数，然后找第k个在左子树还是右子树，然后这样循环下去
- 本来看似是log(k)，但是在最开始统计节点子节点总数的时候是O(n)
- 这样做的优点就满足follow up，每子节点数量已经统计过了，每次插入新值得时候，对父母节点保存的子节点数+1就可以。不需要再次统计了，所以之后的时间复杂度就是log(k)


```java
public class Solution {
    /**
     * @param root: the given BST
     * @param k: the given k
     * @return: the kth smallest element in BST
     */
    public int kthSmallest(TreeNode root, int k) {
        Map<TreeNode, Integer> numOfChildren = new HashMap<>();
        countNodes(root, numOfChildren);
        return quickSelectOnTree(root, k, numOfChildren);
    }
    
    private int countNodes(TreeNode root, Map<TreeNode, Integer> numOfChildren) {
        if (root == null) {
            return 0;
        }
        
        int left = countNodes(root.left, numOfChildren);
        int right = countNodes(root.right, numOfChildren);
        numOfChildren.put(root, left + right + 1);
        return left + right + 1;
    }
    
    private int quickSelectOnTree(TreeNode root, int k, Map<TreeNode, Integer> numOfChildren) {
        if (root == null) {
            return -1;
        }
        
        int left = root.left == null ? 0 : numOfChildren.get(root.left);
        if (left >= k) {
            return quickSelectOnTree(root.left, k, numOfChildren);
        }
        if (left + 1 == k) {
            return root.val;
        }
        
        return quickSelectOnTree(root.right, k - left - 1, numOfChildren);
    }
}
```

####Follow Up
If we could add a count field in the BST node class, it will take O(n) time when we calculate the count value for the whole tree, but after that, it will take O(logn) time when insert/delete a node or calculate the kth smallest element.

- [source1](https://leetcode.com/discuss/43464/what-if-you-could-modify-the-bst-nodes-structure)
- [source2](http://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)
