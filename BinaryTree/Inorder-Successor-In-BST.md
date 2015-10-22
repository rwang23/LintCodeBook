##Inorder Successor in BST

27% Accepted

	Given a binary search tree and a node in it,
    find the in-order successor of that node in the BST.

	Have you met this question in a real interview? Yes
	Example
	Given tree = [2,1] and node = 1:

	  2
	 /
	1
	return node 2.

	Given tree = [2,1,3] and node = 2:

	  2
	 / \
	1   3
	return node 3.

	Note
	If the given node has no in-order successor in the tree, return null.

####Challenge
O(h), where h is the height of the BST.

####Tags Expand
- Binary Search Tree
- Binary Tree

###思路
- 重做

```java
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        TreeNode successor = null;
        while (root != null && root.val != p.val) {
            if (root.val > p.val) {
                successor = root;
                root = root.left;
            } else {
                root = root.right;
            }
        }

        if (root == null) {
            return null;
        }

        if (root.right == null) {
            return successor;
        }

        root = root.right;
        while (root.left != null) {
            root = root.left;
        }

        return root;
    }
}
```
