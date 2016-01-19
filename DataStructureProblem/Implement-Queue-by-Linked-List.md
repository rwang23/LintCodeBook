##Implement Queue by Linked List

	Implement a Queue by linked list. Support the following basic methods:

	enqueue(item). Put a new item in the queue.
	dequeue(). Move the first item out of the queue, return it.
	Have you met this question in a real interview? Yes
	Example
	enqueue(1)
	enqueue(2)
	enqueue(3)
	dequeue() // return 1
	enqueue(4)
	dequeue() // return 2
####Tags Expand
Linked List Queue


####思路
- 自己写ListNode 包含val和next
- 然后就很简单了

```java
public class Queue {

    private ListNode head;
    private ListNode tail;
    private class ListNode {
        int val;
        ListNode next;
        ListNode (int x) {
            val = x;
            next = null;
        }
    }
    public Queue() {
        // do initialize if necessary
        head = tail = null;
    }

    public void enqueue(int item) {
        // Write your code here
        if (head == null) {
            head = new ListNode(item);
            tail = head;
        } else {
            tail.next = new ListNode(item);
            tail = tail.next;
        }
    }

    public int dequeue() {
        // Write your code here
        if (head == null) {
            return -1;
        }
        int val = head.val;
        head = head.next;
        return val;
    }
}
```
