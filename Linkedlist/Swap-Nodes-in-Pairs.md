##Swap Nodes in Pairs

40% Accepted

	Given a linked list, swap every two adjacent nodes and return its head.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->3->4, you should return the list as 2->1->4->3.

####Challenge
Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

#### Tags Expand
- Linked List

####思路
- 如果自己画得比家里乱了可以多设置几个变量，方便理解,本题我最开始就写乱了，后来用了first与second就好了

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
     * @return a ListNode
     */
    public ListNode swapPairs(ListNode head) {
        // Write your code here
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        while (head.next != null && head.next.next != null) {
            ListNode first = head.next;
            ListNode second = head.next.next;
            head.next = second;
            first.next = second.next;
            second.next = first;
            head = first;
        }
        return dummy.next;
    }
}

```
