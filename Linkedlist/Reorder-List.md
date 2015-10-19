##Reorder List

23% Accepted

	Given a singly linked list L: L0→L1→…→Ln-1→Ln,
	reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

	You must do this in-place without altering the nodes' values.



	Have you met this question in a real interview? Yes
	Example
	For example,
	Given 1->2->3->4->null, reorder it to 1->4->2->3->null.

####Tags Expand
- Linked List

####思路
- 拆分，然后后半段翻转，再merge
- 重做

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
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        ListNode tail = reverse(slow.next);
        slow.next = null;

        int index = 0;
        ListNode dummy = new ListNode(0);
        ListNode temp = dummy;
        while (head!=null && tail != null) {
            if (index % 2 == 0) {
                dummy.next = head;
                head = head.next;
            } else {
                dummy.next = tail;
                tail = tail.next;
            }
            dummy = dummy.next;
            index ++;
        }
         if (head != null) {
            dummy.next = head;
        } else {
            dummy.next = tail;
        }
        head = temp.next;
    }

    public ListNode reverse(ListNode head) {
        // write your code here
        if (head == null ) {
            return null;
        }
        ListNode cur = head;
        ListNode reverse = null;
        while (cur != null) {
            ListNode temp = cur.next;
            cur.next = reverse;
            reverse = cur;
            cur = temp;
        }
        return reverse;
    }
}


```
