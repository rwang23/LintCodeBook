##Remove Nth Node From End of List

28% Accepted

	Given a linked list, remove the nth node from the end of list and return its head.

	Have you met this question in a real interview? Yes
	Example
	Given linked list: 1->2->3->4->5->null, and n = 2.

	After removing the second node from the end, the linked list becomes 1->2->3->5->null.
	Note
	The minimum number of nodes in list is n.

####Challenge
- O(n) time

####Tags Expand
- Two Pointers
- Linked List


```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param head: The first node of linked list.
     * @param n: An integer.
     * @return: The head of linked list.
     */
    ListNode removeNthFromEnd(ListNode head, int n) {
        // write your code here
        if (head == null) {
            return null;
        }
        ListNode fast = new ListNode(0);
        fast.next = head;
        head = fast;
        ListNode slow = fast;
        for (int i = 0; i < n && fast.next != null; i++) {
            fast = fast.next;
        }
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        if (slow.next != null) {
            slow.next = slow.next.next;
        }

        return head.next;
    }
}


```
