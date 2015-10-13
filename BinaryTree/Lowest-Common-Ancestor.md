##Lowest Common Ancestor

33% Accepted


	Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes.

	The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.

	Have you met this question in a real interview? Yes
	Example
	For the following binary tree:

	  4
	 / \
	3   7
	   / \
	  5   6
	LCA(3, 5) = 4

	LCA(5, 6) = 7

	LCA(6, 7) = 7

####Tags Expand
- LintCode Copyright
- Binary Tree

####思路
- 参考九章算法
- 在root为根的二叉树中找A,B的LCA:
- 如果找到了就返回这个LCA; 如果只碰到A，就返回A; 如果只碰到B，就返回B; 如果都没有，就返回null
- 通过分治的方法分别去找，找不到返回null,找到一个，比如left，那么left=A;
- 递归进入最底层，从最下面开始寻找
- 每次递归回到调用函数上，就到了上一层，就正在上一层的root上
- *这个题很好的利用了递归* 先到最底层的结点，再进行判断，所以判断函数放在递归函数的后面。如果放在了前面，就是说先判断最上结点


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
     * @param root: The root of the binary search tree.
     * @param A and B: two nodes in a Binary.
     * @return: Return the least common ancestor(LCA) of the two nodes.
     */
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode A, TreeNode B) {
        // write your code here
        if (root == null || root == A || root == B) {
            return root;
        }

        // Divide
        TreeNode left = lowestCommonAncestor(root.left, A, B);
        TreeNode right = lowestCommonAncestor(root.right, A, B);

        // Conquer
        if (left != null && right != null) {
            return root;
        }
        if (left != null) {
            return left;
        }
        if (right != null) {
            return right;
        }
        return null;
    }
}

```
