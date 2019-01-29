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
- 无法直接的分治递归,需要添加一个全局变量
- 如果要直接分支递归,则需要添加一个class,里边包含sum,minSum,minSubtree

####全局变量

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

####直接分治

```java
class ResultType {
    public TreeNode minSubtree;
    public int sum, minSum;
    public ResultType(TreeNode minSubtree, int minSum, int sum) {
        this.minSubtree = minSubtree;
        this.minSum = minSum;
        this.sum = sum;
    }
}

public class Solution {
    /**
     * @param root the root of binary tree
     * @return the root of the minimum subtree
     */
    public TreeNode findSubtree(TreeNode root) {
        ResultType result = helper(root);
        return result.minSubtree;
    }

    public ResultType helper(TreeNode node) {
        if (node == null) {
            return new ResultType(null, Integer.MAX_VALUE, 0);
        }

        ResultType leftResult = helper(node.left);
        ResultType rightResult = helper(node.right);

        ResultType result = new ResultType(
            node,
            leftResult.sum + rightResult.sum + node.val,
            leftResult.sum + rightResult.sum + node.val
        );

        if (leftResult.minSum <= result.minSum) {
            result.minSum = leftResult.minSum;
            result.minSubtree = leftResult.minSubtree;
        }

        if (rightResult.minSum <= result.minSum) {
            result.minSum = rightResult.minSum;
            result.minSubtree = rightResult.minSubtree;
        }

        return result;
    }
}
```
