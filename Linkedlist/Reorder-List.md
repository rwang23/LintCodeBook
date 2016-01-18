##Reorder List

23% Accepted

	Given a singly linked list L: L0→L1→…→Ln-1→Ln,
	reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

	You must do this in-place without altering the nodes' values.

	For example,
	Given 1->2->3->4->null, reorder it to 1->4->2->3->null.

####Tags Expand
- Linked List

####思路
- 拆分，然后后半段翻转，再merge
- 重做 : 完成

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
     * @param head: The head of linked list.
     * @return: void
     */
    public void reorderList(ListNode head) {
        // write your code here
        if (head == null || head.next == null) {
            return;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = head;
        ListNode slow = head;

        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode half = slow.next;
        slow.next = null;
        half = reverseList(half);

        while (head != null && half != null) {
            ListNode next = head.next;
            ListNode secondnext = null;
            secondnext = half.next;
            head.next = half;
            half.next = next;
            head = next;
            half = secondnext;
        }

    }

    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        //ListNode dummy = new ListNode(0);
        ListNode pre = null;

        while (head != null) {
            ListNode next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }

        return pre;
    }
}


```
