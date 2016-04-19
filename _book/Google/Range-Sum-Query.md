##Range Sum Query
	Total Accepted: 7656 Total Submissions: 45053 Difficulty: Medium
	Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

	The update(i, val) function modifies nums by updating the element at index i to val.
	Example:
	Given nums = [1, 3, 5]

	sumRange(0, 2) -> 9
	update(1, 2)
	sumRange(0, 2) -> 8
	Note:
	The array is only modifiable by the update function.
	You may assume the number of calls to update and sumRange function is distributed evenly.

####思路
- SegmentTree
- 以前在写二叉树的时候实现过
- 线段树现在的考法越来越多了,值得注意的数据结构

```java
public class NumArray {

    private class SegmentTree{
        private int sum;
        private SegmentTree left;
        private SegmentTree right;
        private int start;
        private int end;
        SegmentTree(int start, int end) {
            this.start = start;
            this.end = end;
        }
    }

    private SegmentTree root;

    public NumArray(int[] nums) {
        root = buildTree(root, nums, 0, nums.length - 1);
    }

    public SegmentTree buildTree(SegmentTree node, int[] nums, int start, int end) {
        if (start > end) {
            return null;
        }

        node = new SegmentTree(start, end);
        if (start == end) {
            node.sum = nums[start];
            return node;
        }

        int mid = start + (end - start) / 2;
        node.left = buildTree(node.left, nums, start, mid);
        node.right = buildTree(node.right, nums, mid + 1, end);
        node.sum = node.left.sum + node.right.sum;

        return node;
    }

    void update(int i, int val) {
        update(i, val, root);
    }

    void update(int i, int val, SegmentTree node) {

        if (node.start == node.end) {
            node.sum = val;
            return;
        }

        int mid = node.start + (node.end - node.start) / 2;

        if (i <= mid) {
            update(i, val, node.left);
        } else {
            update(i, val, node.right);
        }

        node.sum = node.left.sum + node.right.sum;
    }

    public int sumRange(int i, int j) {
        return sumRange(root, i, j);
    }

    public int sumRange(SegmentTree node, int i, int j) {
        if (i == node.start && j == node.end) {
            return node.sum;
        }

        int mid = node.start + (node.end - node.start) / 2;

        if (j <= mid) {
            return sumRange(node.left, i, j);
        } else if (i > mid) {
            return sumRange(node.right, i , j);
        } else {
            return sumRange(node.left, i, mid) + sumRange(node.right, mid + 1, j);
        }

    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.update(1, 10);
// numArray.sumRange(1, 2);
```
