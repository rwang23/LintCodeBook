##Implement strStr()
[lintcode](https://www.lintcode.com/problem/middle-of-linked-list/description?_from=ladder&&fromId=1)

Middle of Linked List
Find the middle node of a linked list.

Example
Example 1:

Input:  1->2->3
Output: 2
Explanation: return the value of the middle node.
Example 2:

Input:  1->2
Output: 1
Explanation: If the length of list is  even return the value of center left one.
Challenge
If the linked list is in a data stream, can you find the middle without iterating the linked list again?

####思路
- 快慢指针,要想好奇数偶数问题
- 如果是判断 fast != null && fast.next != null 就解决了这个问题

```java
/**
 * Definition for ListNode
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
    /**
     * @param head: the head of linked list.
     * @return: a middle node of the linked list
     */
    public ListNode middleNode(ListNode head) {
        // write your code here
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;

        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }

        return slow;

    }
}
```
