##Remove Duplicates from Sorted List

38% Accepted

	Given a sorted linked list, delete all duplicates such that each element appear only once.

	Have you met this question in a real interview? Yes
	Example
	Given 1->1->2, return 1->2.
	Given 1->1->2->3->3, return 1->2->3.

####Tags Expand
- Linked List

####思路

```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        dummy.next = head;
        ListNode current = dummy;
        while (current != null && current.next != null) {
            ListNode nextone = current.next;
            if (current.val == nextone.val) {
                current.next = nextone.next;
            } else{
                current = current.next;
            }
        }

        return dummy.next;
    }
}

```
