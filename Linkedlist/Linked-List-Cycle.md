##Linked List Cycle

47% Accepted

	Given a linked list, determine if it has a cycle in it.
	Example
	Given -21->10->4->5, tail connects to node index 1, return true

####Challenge
- Can you solve it without using extra space?

####Tags Expand
- Two Pointers
- Linked List

####思路
- 快慢指针，如果相遇，说明有环

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
     * @param head: The first node of linked list.
     * @return: True if it has a cycle, or false
     */
    public boolean hasCycle(ListNode head) {
        // write your code here
        if (head == null) {
            return false;
        }
        ListNode fast = head;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                return true;
            }
        }
        return false;
    }
}



```
