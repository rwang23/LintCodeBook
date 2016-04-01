##Binary Tree Upside Down
	Total Accepted: 9396 Total Submissions: 24745 Difficulty: Medium
	Given a binary tree where all the right nodes are either leaf nodes with a sibling
	 (a left node that shares the same parent node) or empty,
	 flip it upside down and turn it into a tree where the original right nodes turned into left leaf nodes. Return the new root.

	For example:
	Given a binary tree {1,2,3,4,5},
	    1
	   / \
	  2   3
	 / \
	4   5
	return the root of the binary tree [4,5,2,#,#,3,1].
	   4
	  / \
	 5   2
	    / \
	   3   1
	confused what "{1,#,2,3}" means? > read more on how binary tree is serialized on OJ.

####思路
- 首先想到的是,先postorder得到后序遍历的值,再用level order给每个节点找父母
- 然后再从后序遍历的值来进行构建(根据父母关系), iterative
- 这个方法稍微有点麻烦, 但是O(n)时间能完成


####超棒的思路,直接从节点进行改变
[O(n)time, O(1)space](https://leetcode.com/discuss/18410/easy-o-n-iteration-solution-java)

```java
public class Solution {
    public TreeNode upsideDownBinaryTree(TreeNode root) {
        TreeNode curr = root;
        TreeNode prev = null;
        TreeNode next = null;
        TreeNode temp = null;

        while (curr != null) {
            next = curr.left;
            curr.left = temp;
            temp = curr.right;
            curr.right = prev;
            prev = curr;
            curr = next;
        }

        return prev;
    }
}
```

####递归思路

```java
public class Solution {
    public TreeNode UpsideDownBinaryTree(TreeNode root) {
        if(root == null)return null;
        if(root.left == null)return root;
        TreeNode newroot = UpsideDownBinaryTree(root.left);
        root.left.left = root.right;
        root.left.right = root;
        root.right = null;
        root.left = null;
        return newroot;

    }
}
```
