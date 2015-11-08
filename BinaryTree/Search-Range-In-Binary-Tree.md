##Search Range in Binary Search Tree

36% Accepted


	Given two values k1 and k2 (where k1 < k2) and a root pointer to a Binary Search Tree.
    Find all the keys of tree in range k1 to k2.
    i.e. print all x such that k1<=x<=k2 and x is a key of given BST.
    Return all the keys in ascending order.

	Have you met this question in a real interview? Yes
	Example
	If k1 = 10 and k2 = 22, then your function should return [12, 20, 22].

	    20
	   /  \
	  8   22
	 / \
	4   12

####Tags Expand
- Binary Search Tree
- Binary Tree

####思路
- 分治法。 找左子树符合要求的元素，再找右子树符合要求的元素
- 使用了stack 先存大值。 其实也可以不用

```java

public class Solution {

    public ArrayList<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        if(root == null){
            return new ArrayList<Integer>();
        }
        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        search(root, k1,  k2, stack);

        while(!stack.isEmpty()){
            TreeNode cur = stack.peek();
            result.add(cur.val);
            stack.pop();
        }
        return result;
    }

    public void search(TreeNode root, int k1, int k2, Stack<TreeNode> stack){

        if(root == null){
            return;
        }

        search(root.right, k1, k2, stack);

        if(root.val >= k1 && root.val <= k2){
            stack.push(root);
        }
        search(root.left, k1, k2, stack);
    }
}

```

####非递归
- inorder traversal

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
     * @param k1 and k2: range k1 to k2.
     * @return: Return all keys that k1<=key<=k2 in ascending order.
     */
    public ArrayList<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        if(root == null){
            return new ArrayList<Integer>();
        }

        ArrayList<Integer> result = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();

        TreeNode cur = root;
        while(!stack.isEmpty() || cur != null){
            while(cur != null){
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.peek();
            if(cur.val >= k1 && cur.val <= k2) {
                result.add(cur.val);
            }
            stack.pop();
            cur = cur.right;
        }

        return result;
    }
}


```
