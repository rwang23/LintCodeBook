##Reverse Linked List

40% Accepted

	Reverse a linked list.

	Have you met this question in a real interview? Yes
	Example
	For linked list 1->2->3, the reversed linked list is 3->2->1

####Challenge
Reverse it in-place and in one-pass

####Tags Expand
- Linked List


####思路
- 两个头指针 一个cur 找下一个 然后赋予到reverse上

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
     * @return: The new head of reversed linked list.
     */
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
