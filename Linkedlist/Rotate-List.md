##Rotate List

26% Accepted

	Given a list, rotate the list to the right by k places, where k is non-negative.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->3->4->5 and k = 2, return 4->5->1->2->3.

####Tags Expand
- Basic Implementation
- Linked List

####思路
- Two Pointers


```java
/**
 * Definition for singly-linked list.
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
     * @param head: the List
     * @param k: rotate to the right k places
     * @return: the list after rotation
     */
    public ListNode rotateRight(ListNode head, int k) {
        // write your code here
        if (head == null) {
            return null;
        }
        if (head.next == null) {
            return head;
        }
        ListNode fast = head;
        for (int i = 0; i < k && fast.next != null; i++) {
                fast = fast.next;
        }
        ListNode cur = head;
        while (fast.next != null) {
            fast = fast.next;
            cur = cur.next;
        }
        ListNode root = cur.next;
        fast.next = head;
        cur.next = null;

        return root;
    }
}

```
