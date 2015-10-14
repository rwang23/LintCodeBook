##Insertion Sort List

30% Accepted

	Sort a linked list using insertion sort.

	Have you met this question in a real interview? Yes
	Example
	Given 1->3->2->0->null, return 0->1->2->3->null.

####Tags Expand
- Sort
- Linked List

####思路
- 稍微跟数组的有一点不一样
- [Youtube视频思路](https://www.youtube.com/watch?v=_5_v2E0OWVs)
- 链表的基本操作了，搜索并进行相应的插入。数组是从找到目标之后，在前边的K里边从k找到0，而Linkedlist因为无法回到上一个，所以从0开始找找到k。所以要设置一个dummy head

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
     * @return: The head of linked list.
     */
    public ListNode insertionSortList(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode helper = new ListNode(0);
        ListNode pre = helper;
        ListNode cur = head;
        while (cur!=null) {
            ListNode next = cur.next;
            pre = helper;
            while (pre.next!=null && pre.next.val<=cur.val) {
                pre = pre.next;
            }
            cur.next = pre.next;
            pre.next = cur;
            cur = next;
        }
        return helper.next;
    }
}

```
