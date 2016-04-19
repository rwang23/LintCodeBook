##Sort List

27% Accepted

	Sort a linked list in O(n log n) time using constant space complexity.

	Have you met this question in a real interview? Yes
	Example
	Given 1-3->2->null, sort it to 1->2->3->null.

####Tags Expand
- Linked List Merge Sort算法
- [quick sort算法](http://www.jiuzhang.com/solutions/sort-list/)

####思路

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
     * @return: You should return the head of the sorted linked list, using constant space complexity.
     */
    public ListNode sortList(ListNode head) {
        // write your code here
        if (head == null || head.next == null) {
            return head;
        }

        ListNode mid = findmid(head);
        ListNode right = sortList(mid.next);
        mid.next = null; // 这样就断了下半段，可以进行下半段

        ListNode left = sortList(head);
        return mergeTwoLists(left, right);
    }


    public ListNode findmid(ListNode head) {
        if (head == null) {
            return head;
        }
        ListNode fast = head.next; // 找到重点，而不是可能出现的是上一个
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
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

####Merge Sort的模板做法
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
     * @return: You should return the head of the sorted linked list,
     *             using constant space complexity.
     */
    public ListNode sortList(ListNode head) {
        // write your code here
        if (head == null || head.next == null) {
            return head;
        }

        ListNode mid = findMiddle(head);
        ListNode next = mid.next;
        mid.next = null;

        return helper(head, next);
    }

    public ListNode helper(ListNode headA, ListNode headB) {
        if (headB == null) {
            return headA;
        }

        ListNode mid = findMiddle(headA);
        ListNode next = mid.next;
        mid.next = null;
        ListNode left = helper(headA, next);

        mid = findMiddle(headB);
        next = mid.next;
        mid.next = null;
        ListNode right = helper(headB, next);

        return mergeTwoLists(left, right);
    }

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

    public ListNode findMiddle(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode fast = head;
        ListNode slow = head;

        while (fast.next != null && fast.next.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    }
}

```
