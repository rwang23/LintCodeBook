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
- 用Int去表征大小去比较
- 重做

```java
public class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;

        while (head.next != null && head.next.next != null) {
            if (head.next.val == head.next.next.val) {
                int val = head.next.val;
                while (head.next != null && head.next.val == val) {
                    head.next = head.next.next;
                }
            } else {
                head = head.next;
            }
        }

        return dummy.next;
    }
}
```

####原来的看不明白了 又写了一下
- 关键还是在于preNode

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
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        dummy.next = head;
        ListNode preNode = dummy;

        int tempValue = head.val;
        while (head != null) {
            ListNode nextNode = head.next;
            boolean isDuplicates = false;
            while (nextNode != null && tempValue == nextNode.val) {
                nextNode = nextNode.next;
                isDuplicates = true;
            }
            if (isDuplicates) {
                preNode.next = nextNode;
            } else {
                preNode = preNode.next;
            }
            if (nextNode != null) {
                tempValue = nextNode.val;
            }
            head = nextNode;

        }
        return dummy.next;
    }
}
```
