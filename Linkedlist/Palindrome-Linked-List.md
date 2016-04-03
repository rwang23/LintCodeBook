##Palindrome Linked List

30% Accepted

	Implement a function to check if a linked list is a palindrome.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->1, return true

####Challenge
Could you do it in O(n) time and O(1) space?

####Tags Expand
- Linked List

####思路
- 先取中间，注意取中间的时候有两种情况，一种是奇数长度的链表，一种是偶数长度链表
- 然后拆分后边部分，reverse，再比较

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            pre = pre.next;
        }
        pre.next = null;

        slow = reverse(slow);
        while (head != null) {
            if (head.val != slow.val) {
                return false;
            } else {
                head = head.next;
                slow = slow.next;
            }
        }
        return true;
    }

    public ListNode reverse(ListNode head) {
        if (head == null) {
            return head;
        }

        ListNode pre = null;
        ListNode cur = head;

        while (cur != null) {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }

        return pre;
    }
}
```
