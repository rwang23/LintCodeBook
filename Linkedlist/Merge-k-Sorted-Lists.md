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
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {
        // write your code here
        if (lists.size() == 0) {
            return null;
        }
        int len = lists.size();
        for (int i = 1; i < len; i = i + i) {
            for (int j = 0; j < len - i; j = j +i +i) {
                ListNode merge = mergeTwoLists(lists.get(j),lists.get(j+i));
                lists.set(j,merge);
            }
        }
        return lists.get(0);
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
