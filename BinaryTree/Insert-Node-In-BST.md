##Insert Node in a Binary Search Tree

40% Accepted


	Given a binary search tree and a new tree node, insert the node into the tree.
    You should keep the tree still be a valid binary search tree.

	Have you met this question in a real interview? Yes
	Example
	Given binary search tree as follow, after Insert node 6, the tree should be:

	  2             2
	 / \           / \
	1   4   -->   1   4
	   /             / \
	  3             3   6

####Challenge
Can you do it without recursion?

####Tags Expand
- LintCode Copyright
- Binary Search Tree

####思路

----
####非递归解法

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
     * @param node: insert this node into the binary search tree
     * @return: The root of the new binary search tree.
     */
    public TreeNode insertNode(TreeNode root, TreeNode node) {
        // write your code here
        if (node == null) {
            return root;
        }
        if (root == null){
            return node;
        }

        TreeNode cur = root;
        while(cur != null) {
            if (node.val < cur.val){
                if( cur.left != null){
                    cur = cur.left;
                }else{
                    cur.left = node;
                    break;
                }
            }
            if (node.val > cur.val){
                if( cur.right != null){
                    cur = cur.right;
                }else{
                    cur.right = node;
                    break;
                }
            }
            if (node.val == cur.val){
                break;
            }
        }

        return root;



    }
}

```


####递归解法
- 没有写root.val == node.val的情况，是因为如果有等于的情况，就覆盖掉就行，不用添加新的

```java
public class Solution {
    /**
     * @param root: The root of the binary search tree.
     * @param node: insert this node into the binary search tree
     * @return: The root of the new binary search tree.
     */
    public TreeNode insertNode(TreeNode root, TreeNode node) {
        if (root == null) {
            return node;
        }
        if (root.val > node.val) {
            root.left = insertNode(root.left, node);
        } else if (root.val < node.val){
            root.right = insertNode(root.right, node);
        }

        return root;
    }
}
```
