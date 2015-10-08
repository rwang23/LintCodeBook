##Convert Sorted Array to Binary Search Tree With Minimal Height

33% Accepted

	Given a sorted (increasing order) array, Convert it to create a binary tree with minimal height.

	Have you met this question in a real interview? Yes
	Example
	Given [1,2,3,4,5,6,7], return

	     4
	   /   \
	  2     6
	 / \    / \
	1   3  5   7
	Note
	There may exist multiple valid solutions, return any of them.

####Tags Expand
- Cracking The Coding Interview
- Recursion
- Binary Tree

####思路
- 这道题我自己在写的时候在 主函数里边写了一大堆边界条件，然而这并没有必要
- 当开始一个一个 找 length == 1, length == 2 的时候可能就要注意了，肯定不是这么去判断边界条件的

```java
public class Solution {
    /**
     * @param A: an integer array
     * @return: a tree node
     */
    public TreeNode sortedArrayToBST(int[] A) {
        // write your code
        if (A == null || A.length == 0) {
           return null;
        }
        return sortedArrayToBST(A, 0 , A.length - 1);
    }

    public TreeNode sortedArrayToBST(int[] A, int start, int end){
        if (start > end) {
            return null;
        }
        int mid = (start + end) / 2;
        TreeNode next = new TreeNode(A[mid]);
        next.left = sortedArrayToBST(A, start, mid - 1);
        next.right = sortedArrayToBST(A, mid + 1, end);
        return next;
    }
}



```
