##Flatten Binary Tree to Linked List

32% Accepted

    Flatten a binary tree to a fake "linked list" in pre-order traversal.

    Here we use the right pointer in TreeNode as the next pointer in ListNode.

    Have you met this question in a real interview? Yes
    Example
                  1
                   \
         1          2
        / \          \
       2   5    =>    3
      / \   \          \
     3   4   6          4
                         \
                          5
                           \
                            6
    Note
    Don't forget to mark the left child of each node to null.
    Or you will get Time Limit Exceeded or Memory Limit Exceeded.

####Challenge
Do it in-place without any extra memory.

####Tags Expand
- Binary Tree
- Depth First Search

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
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void flatten(TreeNode root) {
        // write your code here
        if (root == null || (root.left == null && root.right == null)) {
            return;
        }

        TreeNode left = root.left;
        flatten(left);
        TreeNode right = root.right;
        flatten(right);

        root.left = null;
        root.right = left;
        while (root.right != null) {
            root = root.right;
        }
        root.right = right;

    }

}

```
