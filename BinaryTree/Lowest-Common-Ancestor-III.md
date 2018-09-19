##Lowest Common Ancestor III
  Given the root and two nodes in a Binary Tree. 
  Find the lowest common ancestor(LCA) of the two nodes.
  The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.
  Return null if LCA does not exist.

###Example
  For the following binary tree:

        4
       / \
      3   7
         / \
        5   6
  LCA(3, 5) = 4

  LCA(5, 6) = 7

  LCA(6, 7) = 7

###Notice
  node A or node B may not exist in tree.
  
  
###思路1
- 这道题跟LCA I 的区别就是 A，B可能不存在在树中，
- 所以可以用一个global variable 来记录结果， 或者建立一个resultType来作为return，这样就能判断出是不是想要的结果
- TreeNode 在树中一定都是unique的，自己写的时候考虑了不unique的情况，但是根本不会发生，位置已经决定了一定是unique的，
- 如果是找只是value相等的情况，那么就一定要考虑非unique的情况

###思路2
- 使用非递归，可以level traversal，每次记录找到点的父节点，并且记录找到A或者B的flag

###思路3
- 使用resultType

####解法
- 使用了global variable
- 这样弄边界条件挺多了，很容易出错
- 使用resultType 更改return type是一个更好的办法， 可以参考[九章推荐解法](https://www.jiuzhang.com/solution/lowest-common-ancestor-iii/#tag-other)


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
    /*
     * @param root: The root of the binary tree.
     * @param A: A TreeNode
     * @param B: A TreeNode
     * @return: Return the LCA of the two nodes.
     */
    TreeNode result = null;

    public TreeNode lowestCommonAncestor3(TreeNode root, TreeNode A, TreeNode B) {
        // write your code here
        if (root == null) {
            return root;
        }
        
        findLCA(root, A, B);

        return result;
    }
    
    public TreeNode findLCA(TreeNode root, TreeNode A, TreeNode B) {
        if (root == null) {
            return null;
        }
        
        TreeNode left = findLCA(root.left, A, B);
        TreeNode right = findLCA(root.right, A, B);
        
        if (left != null && right != null) {
            result = root;
        }
        
        if ((left == A && root == B) || (left == B && root == A)) {
            result = root;
        }
        
        if ((right == A && root == B) || (right == B && root == A)) {
            result = root;
        }
        
        if (root == A && root == B) {
            result = root;
        }
        
        if (root == A) {
            return A;
        }
        
        if (root == B) {
            return B;
        }
        
        return (left != null) ? left : ((right != null) ? right : null);
        
    }
}
```
