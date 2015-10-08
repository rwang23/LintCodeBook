##Binary Tree Postorder Traversal

37% Accepted

	Given a binary tree, return the postorder traversal of its nodes' values.

	Have you met this question in a real interview? Yes
	Example
	Given binary tree {1,#,2,3},

	   1
	    \
	     2
	    /
	   3


	return [3,2,1].

####Challenge
Can you do it without recursion?

####Tags Expand
- Recursion
- Binary Tree
- Binary Tree Traversal

####思路
思路来源 <a href="http://www.cnblogs.com/dolphin0520/archive/2011/08/25/2153720.html">海子：二叉树的非递归遍历</a>

- 要保证根结点在左孩子和右孩子访问之后才能访问，因此对于任一结点P，先将其入栈。
- 如果P不存在左孩子和右孩子，则可以直接访问它；或者P存在左孩子或者右孩子，但是其左孩子和右孩子都已被访问过了，则同样可以直接访问该结点。
- 若非上述两种情况，则将P的右孩子和左孩子依次入栈，这样就保证了每次取栈顶元素的时候，左孩子在右孩子前面被访问，左孩子和右孩子都在根结点前面被访问。
- 具体参考代码注释




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
     * @return: Postorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> postorderTraversal(TreeNode root) {
        // write your code here
        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();

        if(root == null){
            return new ArrayList<Integer>();
        }

        TreeNode cur = root;
        stack.push(root);
        TreeNode pre = null;
        while(!stack.isEmpty()){
            cur = stack.peek();
            /*
            cur.right == pre || cur.left == pre
            如果右子树已经遍历过了，那么肯定就轮到了根节点
            如果左边遍历过了，根据else内容 肯定也遍历了右边，所以此时都遍历过了
             */
            if( (cur.left == null && cur.right == null) || (pre != null && (cur.right == pre || cur.left == pre) ) ){
                result.add(cur.val);
                pre = cur;
                stack.pop();
            }else{
            	/*
            	将右子树与左子树依次入栈，先入右，所以在栈底，会先输出左子树
            	 */
                if(cur.right != null){
                    stack.push(cur.right);
                }
                if(cur.left != null){
                    stack.push(cur.left);
                }
            }


        }

        return result;

    }
}

```
