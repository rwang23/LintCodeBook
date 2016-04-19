##Merge k Sorted Lists

26% Accepted

	Merge k sorted linked lists and return it as one sorted list.

	Analyze and describe its complexity.

	Have you met this question in a real interview? Yes
	Example
	Given lists:

	[
	  2->4->null,
	  null,
	  -1->null
	],
	return -1->2->4->null.

####Tags Expand
- Divide and Conquer
- Linked List
- Heap

####Iterative merge解法

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) {
            return null;
        }
        int size = lists.length;

        for (int len = 1; len < size; len = len + len) {
            for (int i = 0; i + len < size; i = i + len * 2) {
               lists[i] = mergeTwoLists(lists[i], lists[i + len]);
            }
        }
        return lists[0];

    }

    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        ListNode dummy = new ListNode(0);
        dummy.next = l1;
        ListNode pre = dummy;
        while (l1 != null || l2 != null) {
            if (l1 == null) {
                pre.next = l2;
                break;
            }
            if (l2 == null) {
                break;
            }

            if (l1.val > l2.val) {
                ListNode temp = l2.next;
                pre.next = l2;
                l2.next = l1;
                l2 = temp;
                pre = pre.next;
            } else {
                pre = pre.next;
                l1 = l1.next;
            }

        }
        return dummy.next;
    }
}

```

####递归解法
```java
public class Solution {
    /**
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {
        if (lists.size() == 0) {
            return null;
        }
        return mergeHelper(lists, 0, lists.size() - 1);
    }

    private ListNode mergeHelper(List<ListNode> lists, int start, int end) {
        if (start == end) {
            return lists.get(start);
        }

        int mid = start + (end - start) / 2;
        ListNode left = mergeHelper(lists, start, mid);
        ListNode right = mergeHelper(lists, mid + 1, end);
        return mergeTwoLists(left, right);
    }

    private ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (list1 != null && list2 != null) {
            if (list1.val < list2.val) {
                tail.next = list1;
                tail = list1;
                list1 = list1.next;
            } else {
                tail.next = list2;
                tail = list2;
                list2 = list2.next;
            }
        }
        if (list1 != null) {
            tail.next = list1;
        } else {
            tail.next = list2;
        }

        return dummy.next;
    }
}
```


####Heap解法

```java
public class Solution {
    private Comparator<ListNode> ListNodeComparator = new Comparator<ListNode>() {
        public int compare(ListNode left, ListNode right) {
            if (left == null) {
                return 1;
            } else if (right == null) {
                return -1;
            }
            return left.val - right.val;
        }
    };

    public ListNode mergeKLists(ArrayList<ListNode> lists) {
        if (lists == null || lists.size() == 0) {
            return null;
        }

        Queue<ListNode> heap = new PriorityQueue<ListNode>(lists.size(), ListNodeComparator);
        for (int i = 0; i < lists.size(); i++) {
            if (lists.get(i) != null) {
                heap.add(lists.get(i));
            }
        }

        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (!heap.isEmpty()) {
            ListNode head = heap.poll();
            tail.next = head;
            tail = head;
            if (head.next != null) {
                heap.add(head.next);
            }
        }
        return dummy.next;
    }
}
```
