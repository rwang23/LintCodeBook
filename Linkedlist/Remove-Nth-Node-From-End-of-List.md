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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || n <= 0) {
            return head;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;
        for (int i = 0; i < n && fast.next != null; i++) {
            fast = fast.next;
        }
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }

        slow.next = slow.next.next;
        /*
        这里return的是dummy.next
        虽然感觉return head也是可以的
        但是如果 输入是[1] 1
        return head 还是[1]
        dummy.next 就是 null 因为已经进行删除了 但是head还是他本身
         */
        return dummy.next;
    }
}


```
