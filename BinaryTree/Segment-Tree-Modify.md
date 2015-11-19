##Segment Tree Modify

36% Accepted

    For a Maximum Segment Tree,
    which each node has an extra value max to store the maximum value in this node's interval.

    Implement a modify function with three parameter root, index and value to change the node's value with [start, end] = [index, index] to the new given value. Make sure after this change, every node in segment tree still has the max attribute with the correct value.

    Have you met this question in a real interview? Yes
    Example
    For segment tree:

                          [1, 4, max=3]
                        /                \
            [1, 2, max=2]                [3, 4, max=3]
           /              \             /             \
    [1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=3]
    if call modify(root, 2, 4), we can get:

                          [1, 4, max=4]
                        /                \
            [1, 2, max=4]                [3, 4, max=3]
           /              \             /             \
    [1, 1, max=2], [2, 2, max=4], [3, 3, max=0], [4, 4, max=3]
    or call modify(root, 4, 0), we can get:

                          [1, 4, max=2]
                        /                \
            [1, 2, max=2]                [3, 4, max=0]
           /              \             /             \
    [1, 1, max=2], [2, 2, max=1], [3, 3, max=0], [4, 4, max=0]
    Note
    We suggest you finish problem Segment Tree Build and Segment Tree Query first.

####Challenge
Do it in O(h) time, h is the height of the segment tree.

####Tags Expand
- LintCode Copyright
- Binary Tree
- Segment Tree

####思路

- 递归,简单题 O(nlogn)
- 可以简化为一层递归 O(h)

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
     *@param root, index, value: The root of segment tree and
     *@ change the node's value with [index, index] to the new given value
     *@return: void
     */
    public void modify(SegmentTreeNode root, int index, int value) {
        if (root == null || index > root.end || index < root.start) {
            return;
        }
        updatenode(root, index, value);
        root.max= updatemax(root);
    }

    public void updatenode(SegmentTreeNode root, int index, int value) {

        if (root == null || index > root.end || index < root.start) {
            return;
        }

        if (index == root.end && index == root.start) {
            root.max = value;
            return;
        }

        if (index <= root.left.end) {
            updatenode(root.left, index, value);
        }

        if (index >= root.right.start) {
            updatenode(root.right, index, value);
        }

        root.max = Math.max(root.left.max, root.right.max);
    }

    public int updatemax(SegmentTreeNode root) {

        if (root.start == root.end) {
            return root.max;
        }

        int left = updatemax(root.left);
        int right = updatemax(root.right);
        root.max = Math.max(left, right);

        return Math.max(left, right);
    }
}

```

####改变后简化写法
- 就改变了一行
- 取消了Update函数,直接在Updatenode中,置换max
- O(h)

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
     *@param root, index, value: The root of segment tree and
     *@ change the node's value with [index, index] to the new given value
     *@return: void
     */
    public void modify(SegmentTreeNode root, int index, int value) {
        if (root == null || index > root.end || index < root.start) {
            return;
        }
        updatenode(root, index, value);
        //root.max= updatemax(root);
    }

    public void updatenode(SegmentTreeNode root, int index, int value) {

        if (root == null || index > root.end || index < root.start) {
            return;
        }

        if (index == root.end && index == root.start) {
            root.max = value;
            return;
        }

        if (index <= root.left.end) {
            updatenode(root.left, index, value);
        }

        if (index >= root.right.start) {
            updatenode(root.right, index, value);
        }

        root.max = Math.max(root.left.max, root.right.max);
    }

}

```
