##Convert Binary Search Tree to Doubly Linked List

	Convert a binary search tree to doubly linked list with in-order traversal.

	Example
	Given a binary search tree:

	    4
	   / \
	  2   5
	 / \
	1   3
	return 1<->2<->3<->4<->5

####Tags Expand
Linked List


####解法
- 简单的中序遍历
- 一遍遍历,一遍就输出双向链表
- 用非递归也是一样

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
 * Definition for Doubly-ListNode.
 * public class DoublyListNode {
 *     int val;
 *     DoublyListNode next, prev;
 *     DoublyListNode(int val) {
 *         this.val = val;
 *         this.next = this.prev = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param root: The root of tree
     * @return: the head of doubly list node
     */
    DoublyListNode cur = new DoublyListNode(0);
    DoublyListNode dummy = cur;
    DoublyListNode pre = null;

    public DoublyListNode bstToDoublyList(TreeNode root) {
        // Write your code here
        if (root == null) {
            return null;
        }

        bstToDoublyList(root.left);

        cur.next =  new DoublyListNode(root.val);
        pre = cur;
        cur = cur.next;
        cur.prev = pre;

        bstToDoublyList(root.right);

        return dummy.next;
    }
}

```
