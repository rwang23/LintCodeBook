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
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param head a ListNode
     * @return a boolean
     */
    public boolean isPalindrome(ListNode head) {
        // Write your code here
        if (head == null || head.next == null) {
            return true;
        }
        ListNode preslow = new ListNode(0);
        preslow.next = head;
        ListNode fast = head.next;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            preslow = preslow.next;
        }
        ListNode mid = slow.next;
        if (fast == null) { //for the odd number length of linkedlist
            preslow.next = null;
        } else { //for the even number length of linkedlist
            slow.next = null;
        }
        mid = reverse(mid);
        while (head != null && mid != null) {
            if (head.val != mid.val) {
                return false;
            }
            head = head.next;
            mid = mid.next;
        }
        if (head != null || mid != null) {
            return false;
        }
        return true;

    }

    public ListNode reverse(ListNode head) {
        // write your code here
        if (head == null) {
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
