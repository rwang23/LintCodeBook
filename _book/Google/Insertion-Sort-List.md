##Insertion Sort List

	Total Accepted: 67535 Total Submissions: 232356 Difficulty: Medium
	Sort a linked list using insertion sort.

####思路
- insertion思路
- 不过每次insert是从前边来看,不然从后边结点回不到前面结点


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
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        ListNode pre = dummy;
        dummy.next = head;
        ListNode cur = head.next;
        head.next = null;
        while (cur != null) {
            pre = dummy;
            head = dummy.next;
            ListNode next = cur.next;
            cur.next = null;
            while (head != null) {
                if (head.val >= cur.val) {
                    pre.next = cur;
                    cur.next = head;
                    break;
                } else {
                    head = head.next;
                    pre = pre.next;
                }
            }
            if (head == null) {
                pre.next = cur;
            }
            cur = next;
        }
        return dummy.next;
    }
}
```
