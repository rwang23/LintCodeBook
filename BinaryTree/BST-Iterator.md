##Binary Search Tree Iterator

30% Accepted

	Design an iterator over a binary search tree with the following rules:

	Elements are visited in ascending order (i.e. an in-order traversal)
	next() and hasNext() queries run in O(1) time in average.

    Have you met this question in a real interview? Yes
	Example
	For the following binary search tree, in-order traversal by using iterator is [1, 6, 10, 11, 12]

	   10
	 /    \
	1      11
	 \       \
	  6       12

####Challenge
- Extra memory usage O(h), h is the height of the tree.
- Super Star: Extra memory usage O(1)

####Tags Expand
- Binary Search Tree
- Binary Tree
- Non Recursion

####思路


-----
####正常解法
- O(1)time O(n)place
- 可以进一步优化

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
 * Example of iterate a tree:
 * Solution iterator = new Solution(root);
 * while (iterator.hasNext()) {
 *    TreeNode node = iterator.next();
 *    do something for node
 * }
 */
public class Solution {

    private ArrayList<TreeNode> result = new ArrayList<TreeNode>();
    private int count;
    private int size;

    public ArrayList<TreeNode> traverse(TreeNode root){
        ArrayList<TreeNode> temp = new ArrayList<TreeNode>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode cur = root;

        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.peek();
            temp.add(cur);
            stack.pop();
            cur = cur.right;
        }
        return temp;
    }

    //@param root: The root of binary tree.
    public Solution(TreeNode root) {
        // write your code here
        this.result = traverse(root);
        this.count = 0;
        this.size = this.result.size();
    }

    //@return: True if there has next node, or false
    public boolean hasNext() {
        // write your code here
        return (this.count < this.size);
    }

    //@return: return next node
    public TreeNode next() {
        // write your code here
        return result.get(count++);
    }
}

```

####优化
- 优化了memory O(h)
- 将原来的中序遍历分成了两个部分
- 用stack记录parent就可以了, 跟 two sum in BST类似
- 在初始化中，只进行入栈
- 在next中，进行出栈
- 非常精彩的解法


```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */

public class BSTIterator {

    Stack<TreeNode> stack = new Stack<TreeNode>();
    public BSTIterator(TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
            TreeNode cur = stack.pop();
            int result = cur.val;
            if (cur.right != null) {
                cur = cur.right;
                while (cur != null) {
                    stack.push(cur);
                    cur = cur.left;
                }
            }
            return result;
    }
}
```
