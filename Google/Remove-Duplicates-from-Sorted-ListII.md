##Remove Duplicates from Sorted List II

27% Accepted

	Given a sorted linked list, delete all nodes that have duplicate numbers,
    leaving only distinct numbers from the original list.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->3->3->4->4->5, return 1->2->5.
	Given 1->1->1->2->3, return 2->3.

####Tags Expand
Linked List


####思路
- 画图
- 用了三个节点 pre, head, next
- dummy - 1    - 2    - 3 - 3 - 3 - 4 - 5 - 5 - 6 - 6
- pre   - head - next -
- 通过head.val next.val去判断,然后通过pre去删除

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy;
        ListNode next = head.next;

        while (next != null) {
            if (head.val != next.val) {
                pre = pre.next;
                head = head.next;
                next = next.next;
            } else {
                while (next != null && head.val == next.val) {
                    head = head.next;
                    next = next.next;
                }
                pre.next = next;
                head = next;
                if (next != null) {
                    next = next.next;
                }
            }
        }

        return dummy.next;
    }
}
```
