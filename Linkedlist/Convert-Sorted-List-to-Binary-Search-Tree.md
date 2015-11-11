##Convert Sorted List to Binary Search Tree

26% Accepted

	Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

	Have you met this question in a real interview? Yes
	Example
	               2
	1->2->3  =>   / \
	             1   3
####Tags Expand
- Recursion
- Linked List

####Challenge
- O(n)

####思路
- 第一种直接的方法是把linkedlist 转化为数组,然后通过数组的方法得到BST 时间O(n) 但是空间也是O(n)
- 另一种分治的直接方法就是找到中间节点作为二叉树的root节点，然后分别对左右链表递归调用分别生成左子树和右子树。时间复杂度O(N*lgN)
- 上面的方法是一种自顶向下的方法，先找到root然后对左右子树分别递归调用。
- 但是我们需要算法复杂度为O(N)。需要自底向上
- 这时候就要利用到树的中序遍历了，按照递归中序遍历的顺序对链表结点一个个进行访问，而我们要构造的二分查找树正是按照链表的顺序来的。思路就是先对左子树进行递归，然后将当前结点作为根，迭代到下一个链表结点，最后在递归求出右子树即可。整体过程就是一次中序遍历，时间复杂度是O(n)，空间复杂度是栈空间O(logn)

```java
public class Solution {
    private ListNode current;

    private int getListLength(ListNode head) {
        int size = 0;

        while (head != null) {
            size++;
            head = head.next;
        }

        return size;
    }

    public TreeNode sortedListToBST(ListNode head) {
        int size;

        current = head;
        size = getListLength(head);

        return sortedListToBSTHelper(size);
    }

    public TreeNode sortedListToBSTHelper(int size) {
        if (size <= 0) {
            return null;
        }

        TreeNode left = sortedListToBSTHelper(size / 2);
        TreeNode root = new TreeNode(current.val);
        current = current.next;
        TreeNode right = sortedListToBSTHelper(size - 1 - size / 2);

        root.left = left;
        root.right = right;

        return root;
    }
}
```
