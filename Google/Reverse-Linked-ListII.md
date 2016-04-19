##Reverse Linked List II

29% Accepted

	Reverse a linked list from position m to n.

	Have you met this question in a real interview? Yes
	Example
	Given 1->2->3->4->5->NULL, m = 2 and n = 4, return 1->4->3->2->5->NULL.

	Note
	Given m, n satisfy the following condition: 1 ≤ m ≤ n ≤ length of list.

####Challenge
Reverse it in-place and in one-pass

####Tags Expand
- Linked List

####思路
- 就是reverse的方法
- 注意边界条件，当n,m大于链表长度的情况
- reverse的方法就是把当前节点下个节点存起来，再把该当前指向上一个节点，然后更新上个节点是什么，当前节点是什么，以此循环
- 该题需要多次练习，去练习写法和边界条件

####Reverse

	ListNode temp = cur.next;
	cur.next = reverse;
	reverse = cur;
	cur = temp;

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
     * @param ListNode head is the head of the linked list
     * @oaram m and n
     * @return: The head of the reversed ListNode
     */
    public ListNode reverseBetween(ListNode head, int m , int n) {
        // write your code
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        for (int i = 1; i < m; i++) {
            if (head.next == null) {
                return dummy.next;
            }
            head = head.next;
        }
        ListNode pre = head;
        ListNode last = head.next;
        head = head.next;
        ListNode prem = null;
        for (int i = m; i <= n; i++) {
            if (head == null) {
                return dummy.next;
            }
            ListNode temp = head.next;
            head.next = prem;
            prem = head;;
            head = temp;
        }
        last.next = head;
        pre.next = prem;
        return dummy.next;

    }
}

```
