##Segment Tree Query

34% Accepted

	For an integer array (index from 0 to n-1, where n is the size of this array),
	in the corresponding SegmentTree, each node stores an extra attribute max to denote the maximum number in the interval of the array (index from start to end).

	Design a query method with three parameters root, start and end, find the maximum number in the interval [start, end] by the given root of segment tree.

	Have you met this question in a real interview? Yes
	Example
	For array [1, 4, 2, 3], the corresponding Segment Tree is:

	                  [0, 3, max=4]
	                 /             \
	          [0,1,max=4]        [2,3,max=3]
	          /         \        /         \
	   [0,0,max=1] [1,1,max=4] [2,2,max=2], [3,3,max=3]
	query(root, 1, 1), return 4

	query(root, 1, 2), return 4

	query(root, 2, 3), return 3

	query(root, 0, 2), return 4

	Note
	It is much easier to understand this problem if you finished Segment Tree Build first.

####Tags Expand
LintCode Copyright Binary Tree Segment Tree

####思路
- 这道题很简单,自己写的时候二了, debug了半天,结果没想到是最后的return写错了一点,一直没有去看return,导致这道题花费了五十分钟

```java
/**
 * Definition of SegmentTreeNode:
 * public class SegmentTreeNode {
 *     public int start, end, max;
 *     public SegmentTreeNode left, right;
 *     public SegmentTreeNode(int start, int end, int max) {
 *         this.start = start;
 *         this.end = end;
 *         this.max = max
 *         this.left = this.right = null;
 *     }
 * }
 */
public class Solution {
    /**
     *@param root, start, end: The root of segment tree and
     *                         an segment / interval
     *@return: The maximum number in the interval [start, end]
     */

    public int query(SegmentTreeNode root, int start, int end) {
        // write your code here
        if (root == null) {
            return 0;
        }
        if (end > root.end) {
            end = root.end;
        }
        if (start < root.start) {
            start = root.start;
        }
        if ((root.left == null && root.right == null) || (root.start == start && root.end == end)) {
            return root.max;
        }

        int max = Integer.MIN_VALUE;
        int leftend = root.left.end;
        int leftstart = root.left.start;
        int rightstart = root.right.start;
        int rightend = root.right.end;

        if (start >= leftstart && end <= leftend) {
             max = Math.max(query(root.left, start, end), max);
        }

        if (start >= rightstart && end <= rightend){
            max = Math.max(query(root.right, start, end), max);
        }

        if (start <= leftend && end >= rightstart) {
            int localmax = Math.max(query(root.left, start, leftend), query(root.right, rightstart, end) );
            max = Math.max(localmax, max);
        }

        return max;
    }
}

```

####一个特别简便的写法但稍慢的写法
- 根本不在乎是否在左右子树,都去找,大不了start end跟子树的start end不达标,返回0就行
- 这种方法因为没有筛选左右子树,所以时间会慢一倍左右,但是写起来非常简便

```java
public class Solution {
    public int query(SegmentTreeNode root, int start, int end) {
        if (root == null || start > root.end || end < root.start) {
            return 0;
        }
        if (root.start == root.end) {
            return root.max;
        }
        int mid = ((root.start + root.end) / 2);
        return Math.max(query(root.left, start, end), query(root.right, start, end));
    }
}
```
