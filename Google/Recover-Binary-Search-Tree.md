##Recover Binary Search Tree

	Two elements of a binary search tree (BST) are swapped by mistake.

	Recover the tree without changing its structure.

	Note:
	A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?
	confused what "{1,#,2,3}" means? > read more on how binary tree is serialized on OJ.

####Tags
Binary Tree

####思路
- O(n)空间的解法比较直观，中序遍历一遍以后排序，重新赋值一遍即可，这个解法可以面向n个元素错位的情况。但是对于O(1)空间的解法
- 不用O(n)空间,就使用递归用法 (貌似不妥)

```java
public class Solution {
    private TreeNode firstElement = null;
    private TreeNode secondElement = null;
    private TreeNode lastElement = new TreeNode(Integer.MIN_VALUE);

    private void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        traverse(root.left);
        if (firstElement == null && root.val < lastElement.val) {
            firstElement = lastElement;
        }
        if (firstElement != null && root.val < lastElement.val) {
            secondElement = root;
        }
        lastElement = root;
        traverse(root.right);
    }

    public void recoverTree(TreeNode root) {
        // traverse and get two elements
        traverse(root);
        // swap
        int temp = firstElement.val;
        firstElement.val = secondElement.val;
        secondElement.val = temp;
    }
}
```

