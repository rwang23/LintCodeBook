##Moving Average from Data Stream
	Total Accepted: 1287 Total Submissions: 1863 Difficulty: Easy
	Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

	For example,
	MovingAverage m = new MovingAverage(3);
	m.next(1) = 1
	m.next(10) = (1 + 10) / 2
	m.next(3) = (1 + 10 + 3) / 3
	m.next(5) = (10 + 3 + 5) / 3

####思路
- 使用listnode,方便的话直接就用queueLe

```java
public class MovingAverage {

    /** Initialize your data structure here. */
    class ListNode {
        private ListNode next;
        private int val;
        ListNode(int val) {
            this.val = val;
        }
    }
    private int capacity;
    private int size;
    private int sum;
    ListNode head;
    ListNode tail;

    public MovingAverage(int size) {
        this.capacity = size;
        this.size = 0;
        head = tail = null;
        this.sum = 0;
    }

    public double next(int val) {
        sum += val;
        if (size < capacity) {
            if (head == null) {
                head = new ListNode(val);
                tail = head;
            } else {
                tail.next = new ListNode(val);
                tail = tail.next;
            }
            size++;
        } else {
            sum -= head.val;
            head = head.next;
            tail.next = new ListNode(val);
            tail = tail.next;
        }
        return (double) (sum) / size;
    }
}

/**
 * Your MovingAverage object will be instantiated and called as such:
 * MovingAverage obj = new MovingAverage(size);
 * double param_1 = obj.next(val);
 */
```
