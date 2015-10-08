##Construct Binary Tree from Preorder and Inorder Traversal

27% Accepted


	Given preorder and inorder traversal of a tree, construct the binary tree.

	Have you met this question in a real interview? Yes
	Example
	Given in-order [1,2,3] and pre-order [2,1,3], return a tree:

	  2
	 / \
	1   3
	Note
	You may assume that duplicates do not exist in the tree.

####Tags Expand
- Binary Tree

####解法
- 基本思路，参考[Youtube视频教程](https://www.youtube.com/watch?v=2OYj9-NjBno)
- 使用了hash map 去储存数组， 很棒的方法， 构造一个函数，每次都能把要取的部分数组值的下标传过去
- 当is>ie的时候，一定是没有左子树，而ps>pe的时候，一定是没有右子树
- preorder每次的第一个，一定是根节点，然后去inorder的此节点，节点左边的就是左子树，节点右边就是右子树，在通过已经确定的左右子树的大小去确定postorder的节点
- 传参数的下标的确定，一定记得画图去验证，否则很容易出错

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
     *@param inorder : A list of integers that inorder traversal of a tree
     *@param postorder : A list of integers that postorder traversal of a tree
     *@return : Root of a tree
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (inorder == null || preorder == null || inorder.length != preorder.length) {
            return null;
        }
        HashMap<Integer, Integer> hm = new HashMap<Integer,Integer>();
        for (int i=0;i<inorder.length;i++) {
            hm.put(inorder[i], i);
        }
        return buildTree(inorder, 0, inorder.length-1, preorder, 0, preorder.length-1,hm);
    }

    private TreeNode buildTree(int[] inorder, int is, int ie, int[] preorder, int ps, int pe, HashMap<Integer,Integer> hm){
        if (ps > pe || is > ie) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[ps]);
        int ri = hm.get(preorder[ps]);

        root.left = buildTree(inorder, is, ri-1, preorder, ps+1, ps+ri-is, hm);
        root.right = buildTree(inorder, ri+1, ie, preorder, ps+ri-is+1, pe, hm);
        return root;
    }

}

```
