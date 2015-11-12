##Intersection of Two Linked Lists

####Leetcode

	Write a program to find the node at which the intersection of two singly linked lists begins.


	For example, the following two linked lists:

	A:          a1 → a2
	                   ↘
	                     c1 → c2 → c3
	                   ↗
	B:     b1 → b2 → b3
	begin to intersect at node c1.


	Notes:

	If the two linked lists have no intersection at all, return null.
	The linked lists must retain their original structure after the function returns.
	You may assume there are no cycles anywhere in the entire linked structure.
	Your code should preferably run in O(n) time and use only O(1) memory.

####思路
- 从长度入手,如果两个链表不等长,则补齐到等长开始找
- 比较linkedlist是否相等,不能光从value值,还需要比较之后next的所有值
- 有深拷贝的思想

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
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {

        ListNode dummy1 = new ListNode(0);
        ListNode dummy2 = new ListNode(0);
        dummy1.next = headA;
        dummy2.next = headB;

        int size1 = 0;
        int size2 = 0;
        while (headA != null) {
            headA = headA.next;
            size1++;
        }
        while (headB != null) {
            headB = headB.next;
            size2++;
        }

        headA = dummy1.next;
        headB = dummy2.next;

        if (size1 > size2) {
            int extra = size1 - size2;
            for (int i = 0; i < extra; i++) {
                headA = headA.next;
            }
        }

        if (size2 > size1) {
            int extra = size2 - size1;
            for (int i = 0; i < extra; i++) {
                headB = headB.next;
            }
        }

        while (headA != null && headB != null) {
            if (isSameNode(headA, headB)) {
                return headA;
            }
            headA = headA.next;
            headB = headB.next;
        }

        return null;

    }

    public boolean isSameNode(ListNode A, ListNode B) {
        if (A == null && B == null) {
            return true;
        }
        if (A == null || B == null ) {
            return false;
        }

        if (A.val == B.val) {
            return isSameNode(A.next, B.next);
        } else {
            return false;
        }
    }
}
```
