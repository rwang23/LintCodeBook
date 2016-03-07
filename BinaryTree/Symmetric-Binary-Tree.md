##Symmetric Binary Tree

38% Accepted

	Given a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

	Have you met this question in a real interview? Yes
	Example
	    1
	   / \
	  2   2
	 / \ / \
	3  4 4  3
	is a symmetric binary tree.

	    1
	   / \
	  2   2
	   \   \
	   3    3
	is not a symmetric binary tree.

####Challenge
Can you solve it both recursively and iteratively?

####Tags Expand
Binary Tree



####非递归思路
- in order traversal存入数组,观察数组,就能判断是不是对称的
- 判断两个treenode是否相等,不能直接比较,因为不是存在内存中一个位置
- 要判断两个treenode结点值是否相等,并且 a的左子树的值是否等于b的右子树,a的右子树值是否等于b的左子树
- 判断的条件有很多,不光上边说的值相不相等,还存在a没有子树,右有子树的情况,而且每次判断子树值的时候都要先判断子树是否为空
- 所以这里我有了一点小trick,先赋好值,再判断


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
     * @param root, the root of binary tree.
     * @return true if it is a mirror of itself, or false.
     */
    public boolean isSymmetric(TreeNode root) {
        // Write your code here
        if (root == null) {
            return true;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode cur = root;
        //queue.offer(cur);
        ArrayList<TreeNode> nums = new ArrayList<TreeNode>();

        while(!stack.isEmpty() || cur != null) {
            while (cur != null) {
                stack.push(cur);
                cur = cur.left;
            }

            cur = stack.peek();
            nums.add(cur);
            stack.pop();
            cur = cur.right;
        }

        int size = nums.size();
        for (int i = 0, j = size - 1; i < j; i++, j--) {
            TreeNode temp1 = nums.get(i);
            TreeNode temp2 = nums.get(j);
            if (!isEqual(temp1, temp2)) {
                return false;
            }
        }

        return true;
    }

    public boolean isEqual(TreeNode node1, TreeNode node2) {
        if ( !(node1.val == node2.val)) {
            return false;
        }

        int node1_left_val = Integer.MIN_VALUE;
        int node1_right_val = Integer.MIN_VALUE;
        int node2_left_val = Integer.MIN_VALUE;
        int node2_right_val = Integer.MIN_VALUE;

        if (node1.left != null) {
            node1_left_val = node1.left.val;
        }
        if (node1.right != null) {
            node1_right_val = node1.right.val;
        }
        if (node2.left != null) {
            node2_left_val = node2.left.val;
        }
        if (node2.right != null) {
            node2_right_val = node2.right.val;
        }

        return (node1_left_val == node2_right_val) && (node1_right_val == node2_left_val);
    }

}

```


####递归思路
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }

        return isSymmetric(root.left, root.right);
    }
    public boolean isSymmetric(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }
        if (left == null || right == null) {
            return false;
        }
        if (left.val != right.val) {
            return false;
        }
        return isSymmetric(left.left, right.right) && isSymmetric(left.right, right.left);

    }
}
```
