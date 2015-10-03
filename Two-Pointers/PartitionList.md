## Partition List

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

    Given 1->4->3->2->5->2->null and x = 3,
    return 1->2->2->4->3->5->null.

####Tags: Two Pointers; Linked List

####思路
- 创建了两个链表 分别储存左边小于的 以及 右边大于的
- 太精辟
- leftDummmy存左边第一个节点
- rightDummy存右边第一个节点
- 比较大小存完之后，讲量表连接起来
- 记得把right.next=null 避免溢出


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
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return null;
        }
        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        ListNode left = leftDummy, right = rightDummy;

        while (head != null) {
            if (head.val < x) {
                left.next = head;
                left = head;
            } else {
                right.next = head;
                right = head;
            }
            head = head.next;
        }

        right.next = null;
        left.next = rightDummy.next;
        return leftDummy.next;
    }
}
```

