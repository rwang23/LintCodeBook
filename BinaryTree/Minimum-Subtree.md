##Minimum Subtree
Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.

####Example
  Given a binary tree:

       1
     /   \
   -5     2
   / \   /  \
  0   2 -4  -5 
  return the node 1.
  
####解法
- 最开始写的解法里边的getSum有这么一段，每次判断左右，这样就导致了如果子节点是空，那么sum就是0，就会比其他sum都小，导致错误
- 既然已经分治，那么这里就不需要单独对左右子树了

```java
        if (left <= min) {
            min = left;
            minNode = root.left;
        }
        if (right <= min) {
            min = right;
            minNode = root.right;
        }
```

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
     * @param root: the root of binary tree
     * @return: the root of the minimum subtree
     */
    int min = Integer.MAX_VALUE;
    TreeNode minNode = null;
    public TreeNode findSubtree(TreeNode root) {
        // write your code here
        if (root == null) {
            return root;
        }
        
        minNode = root;
        getSum(root);
        return minNode;
    }
    
    public int getSum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int left = getSum(root.left);
        int right = getSum(root.right);
        int sum = left + right + root.val;

        if (sum <= min) {
            min = sum;
            minNode = root;
        }
        
        return sum;
    }
}
```
