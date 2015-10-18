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
    /**
     * @param ListNode head is the head of the linked list
     * @return: ListNode head of linked list
     */
    public static ListNode deleteDuplicates(ListNode head) {
        // write your code here
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        while (head.next != null && head.next.next != null) {
            if (head.next.val == head.next.next.val) {
                head.next.next = head.next.next.next;
            } else {
                head = head.next;
            }
        }
        return dummy.next;
    }
}

```
