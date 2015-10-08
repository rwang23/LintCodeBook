##Construct Binary Tree from Inorder and Postorder Traversal

29% Accepted


	Given inorder and postorder traversal of a tree, construct the binary tree.

	Have you met this question in a real interview? Yes
	Example
	Given inorder [1,2,3] and postorder [1,3,2], return a tree:

	  2
	 / \
	1   3
	Note
	You may assume that duplicates do not exist in the tree.

####Tags Expand
- Binary Tree

####思路
- 基本思路，参考[Youtube视频教程](https://www.youtube.com/watch?v=k2dvEJoHVEM)
- 使用了hash map 去储存数组， 很棒的方法， 构造一个函数，每次都能把要取的部分数组值的下标传过去
- 当is>ie的时候，一定是没有左子树，而ps>pe的时候，一定是没有右子树
- postorder每次的最后一个，一定是根节点，然后去inorder的此节点，节点左边的就是左子树，节点右边就是右子树，在通过已经确定的左右子树的大小去确定postorder的节点
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
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder == null || postorder == null || inorder.length != postorder.length) {
            return null;
        }
        HashMap<Integer, Integer> hm = new HashMap<Integer,Integer>();
        for (int i=0;i<inorder.length;++i) {
            hm.put(inorder[i], i);
        }
        return buildTree(inorder, 0, inorder.length-1, postorder, 0, postorder.length-1,hm);
    }

    private TreeNode buildTree(int[] inorder, int is, int ie, int[] postorder, int ps, int pe, HashMap<Integer,Integer> hm){
        if (ps>pe || is>ie) {
            return null;
        }
        TreeNode root = new TreeNode(postorder[pe]);
        int ri = hm.get(postorder[pe]);
        root.left = buildTree(inorder, is, ri-1, postorder, ps, ps+ri-is-1, hm);
        root.right = buildTree(inorder,ri+1, ie, postorder, ps+ri-is, pe-1, hm);
        return root;
    }

}

```
