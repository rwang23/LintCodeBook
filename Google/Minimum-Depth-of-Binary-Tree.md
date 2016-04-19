##Minimum Depth of Binary Tree

31% Accepted

	Given a binary tree, find its minimum depth.

	The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

	Have you met this question in a real interview? Yes
	Example
	Given a binary tree as follow:

	        1

	     /     \

	   2       3

	          /    \

	        4      5

	The minimum depth is 2

####Tags Expand
- Depth First Search

####思路
- 还是分治思想
- 但是如果出现了 这样的形状，就不能是1，因为要找最近叶子节点，现在没有找到，所以这个时候要返回右边子树的深度


	1
	 \
	   2
	    \
	     3


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
     * @param root: The root of binary tree.
     * @return: An integer.
     */
    public int minDepth(TreeNode root) {
        // write your code here
        if(root == null){
            return 0;
        }

        int left = minDepth(root.left);
        int right = minDepth(root.right);

        if(left == 0 && right != 0 ){
            return right + 1;
        }else if(left != 0 && right == 0){
            return left + 1;
        }else{
            return Math.min(left, right) + 1;
        }

    }
}

```
###非递归
- level order traversal

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
     * @param root: The root of binary tree.
     * @return: An integer.
     */
    public int minDepth(TreeNode root) {
        // write your code here
        if(root == null){
            return 0;
        }

        Queue<TreeNode> queue = new LinkedList<TreeNode>();

        TreeNode cur = root;
        queue.offer(root);
        int depth = 0;

        while(queue.peek() != null){
            int size = queue.size();
            depth++;
            for(int i = 0; i < size; i++){
                cur = queue.peek();
                if(cur.left == null && cur.right == null) {
                    return depth;
                }
                if(cur.left != null){
                    queue.offer(cur.left);
                }
                if(cur.right != null){
                    queue.offer(cur.right);
                }
                queue.poll();
            }

        }
        return depth;
    }
}

```
