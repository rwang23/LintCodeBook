Palindrome Linked List

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
public class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        ListNode second;
        if (fast.next != null) {
            second = slow.next.next;
        } else {
            second = slow.next;
        }
        slow.next = null;

        ListNode reverseNode = reverse(second);
        ListNode cur = dummy.next;

        while (cur != null) {
            if (cur.val != reverseNode.val) {
                return false;
            }
            cur = cur.next;
            reverseNode = reverseNode.next;
        }
        return true;
    }
    public ListNode reverse(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode pre = null;
        while (head != null) {
            ListNode temp = head.next;
            head.next = pre;
            pre = head;
            head = temp;
        }
        return pre;
    }
}

```
