##Max Tree

28% Accepted

	Given an integer array with no duplicates. A max tree building on this array is defined as follow:

	The root is the maximum number in the array
	The left subtree and right subtree are the max trees of the subarray divided by the root number.
	Construct the max tree by the given array.

	Have you met this question in a real interview? Yes
	Example
	Given [2, 5, 6, 0, 3, 1], the max tree constructed by this array is:

	    6
	   / \
	  5   3
	 /   / \
	2   0   1

####Challenge
- O(n) time and memory.

####Tags Expand
- LintCode Copyright
- Stack
- Cartesian Tree

####Brute Force递归法，nlog(n)
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
     * @param A: Given an integer array with no duplicates.
     * @return: The root of max tree.
     */
    public TreeNode maxTree(int[] A) {
        // write your code here
        if (A == null || A.length == 0) {
            return null;
        }
        return maxTree(A, 0, A.length - 1);
    }

    public TreeNode maxTree(int[] A, int start, int end) {
        if (start > end) {
            return null;
        }

        int maxIndex = findMax(A, start, end);
        TreeNode root = new TreeNode(A[maxIndex]);
        root.left = maxTree(A, start, maxIndex - 1);
        root.right = maxTree(A, maxIndex + 1, end);
        return root;

    }

    public int findMax(int[] A, int start, int end) {
        int max = Integer.MIN_VALUE;
        int index = start;
        for (int i = start; i < end + 1; i++) {
            if (A[i] >= max) {
                max = A[i];
                index = i;
            }
        }
        return index;
    }
}

```


####单增栈解法
- 重做

```java
public class Solution {
  /**
   * @param A
   *            : Given an integer array with no duplicates.
   * @return: The root of max tree.
   */
  public static TreeNode maxTree(int[] A) {
    // write your code here
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode root = null;
    for (int i = 0; i <= A.length; i++) {
      TreeNode right = i == A.length ? new TreeNode(Integer.MAX_VALUE)
          : new TreeNode(A[i]);
      while (!stack.isEmpty()) {
        if (right.val > stack.peek().val) {
          TreeNode nodeNow = stack.pop();
          if (stack.isEmpty()) {
            right.left = nodeNow;
          } else {
            TreeNode left = stack.peek();
            if (left.val > right.val) {
              right.left = nodeNow;
            } else {
              left.right = nodeNow;
            }
          }
        } else
          break;
      }
      stack.push(right);
    }
    return stack.peek().left;
  }
}
```
