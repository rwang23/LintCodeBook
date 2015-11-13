##Remove Duplicates from Unsorted List

57% Accepted

	Write code to remove duplicates from an unsorted linked list.

	Have you met this question in a real interview? Yes
	Example
	Given 1->3->2->1->4.

	Return 1->3->2->4

####Challenge
- (hard) How would you solve this problem if a temporary buffer is not allowed? In this case, you don't need to keep the order of nodes.

####Tags Expand
Linked List


####简单算法

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
     * @param head: The first node of linked list.
     * @return: head node
     */
    public ListNode removeDuplicates(ListNode head) {
        // Write your code here
        if (head == null) {
            return null;
        }
        ListNode cur = head;
        HashSet<Integer> temp = new HashSet<Integer>();
        temp.add(head.val);
        while (head.next != null) {
            if (temp.contains(head.next.val)) {
                head.next = head.next.next;
            } else {
                temp.add(head.next.val);
                head = head.next;
            }
        }
        return cur;
    }
}

```

####O(1) space思路
1. This is the simple way where two loops are used. Outer loop is used to pick the elements one by one and inner loop compares the picked element with rest of the elements.
2. In general, Merge Sort is the best suited sorting algorithm for sorting linked lists efficiently.
1)  Sort the elements using Merge Sort. We will soon be writing a post about sorting a linked list. O(nLogn)
2)  Remove duplicates in linear time using the algorithm for removing duplicates in sorted Linked List. O(n)

Please note that this method doesn’t preserve the original order of elements.

Time Complexity: O(nLogn)
