##Implement Queue by Linked List II

	Implement a Queue by linked list.

	Provide the following basic methods:

	push_front(item). Add a new item to the front of queue.
	push_back(item). Add a new item to the back of the queue.
	pop_front(). Move the first item out of the queue, return it.
	pop_back(). Move the last item out of the queue, return it.
	Have you met this question in a real interview? Yes
	Example
	push_front(1)
	push_back(2)
	pop_back() // return 2
	pop_back() // return 1
	push_back(3)
	push_back(4)
	pop_front() // return 3
	pop_front() // return 4

####Tags Expand
Linked List Queue

####思路
- 构造双向链表,问题就变得简单很多
- 但是双向链表一定要注意,如果断一个点的话,它的next 和 prev都要断, 否则就要出现问题

```java
public class Dequeue {

    private ListNode head;
    private ListNode tail;
    private class ListNode {
        int val;
        ListNode next;
        ListNode prev;
        ListNode(int x) {
            this.val = x;
            next = null;
            prev = null;
        }
    }
    public Dequeue() {
        // do initialize if necessary
        this.head = null;
        this.tail = null;
    }

    public void push_front(int item) {
        // Write your code here
        if (head == null || tail == null) {
            head = new ListNode(item);
            tail = head;
        } else {
            tail.next = new ListNode(item);
            ListNode cur = tail;
            tail = tail.next;
            tail.prev = cur;
        }
    }

    public void push_back(int item) {
        // Write your code here
        if (head == null || tail == null) {
            head = new ListNode(item);
            tail = head;
        } else {
            ListNode newhead = new ListNode(item);
            newhead.next = head;
            head.prev = newhead;
            head = newhead;
        }
    }

    public int pop_front() {
        // Write your code here
        int val = Integer.MAX_VALUE;
        if (head != null || tail == null) {
            val = tail.val;
            ListNode pre = tail.prev;
            //pre.next = null;
            tail = pre;
            if (tail != null) {
                tail.next = null;
            }

        }
        return val;
    }

    public int pop_back() {
        // Write your code here
        int val = Integer.MAX_VALUE;
        if (head != null || tail == null) {
            val = head.val;
            ListNode next = head.next;
            head = next;
            if (head != null) {
                head.prev = null;
            }

        }
        return val;
    }
}
```
