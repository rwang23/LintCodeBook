##Merge Two Sorted Lists

38% Accepted

	Merge two sorted (ascending) linked lists and return it as a new sorted list.
    The new sorted list should be made by splicing together the nodes of the two lists and sorted in ascending order.

	Have you met this question in a real interview? Yes
	Example
	Given 1->3->8->11->15->null, 2->null , return 1->2->3->8->11->15->null.

####Tags Expand
Linked List

####思路
- 两个比较，然后merge，如果一个已经为空，直接赋予mergelist就可以


####创建一个新的list 空间O(n)
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
     * @param ListNode l1 is the head of the linked list
     * @param ListNode l2 is the head of the linked list
     * @return: ListNode head of linked list
     */
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // write your code here
        ListNode mergelist = new ListNode(0);
        ListNode head = mergelist;
        while (true) {
            if (l1 == null) {
                mergelist.next = l2;
                break;
            } else if (l2 == null) {
                mergelist.next = l1;
                break;
            }
            if (l1.val >= l2.val) {
                mergelist.next = l2;
                l2 = l2.next;
            } else {
                mergelist.next = l1;
                l1 = l1.next;
            }
            mergelist = mergelist.next;
        }
        return head.next;

    }
}

```

####在原来的l1上做合并 空间O(1)
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = l1;
        ListNode pre = dummy;
        while (l1 != null || l2 != null) {
            if (l1 == null) {
                pre.next = l2;
                break;
            }
            if (l2 == null) {
                break;
            }

            if (l1.val > l2.val) {
                ListNode temp = l2.next;
                pre.next = l2;
                l2.next = l1;
                l2 = temp;
                pre = pre.next;
            } else {
                pre = pre.next;
                l1 = l1.next;
            }

        }
        return dummy.next;
    }
}
```
