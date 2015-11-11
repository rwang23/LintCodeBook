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
	If you are given an array, the problem is quite straightforward.
	But things get a little more complicated when you have a singly linked list instead of an array. Now you no longer have random access to an element in O(1) time.
	Therefore, you need to create nodes bottom-up, and assign them to its parents.
	The bottom-up approach enables us to access the list in its order at the same time as creating nodes.

####解法
- 来自九章
- 很难理解

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
