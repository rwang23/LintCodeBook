##Implement Stack by Two Queues

	Implement a stack by two queues. The queue is first in first out (FIFO). That means you can not directly pop the last element in a queue.

	Have you met this question in a real interview? Yes
	Example
	push(1)
	pop()
	push(2)
	isEmpty() // return false
	top() // return 2
	pop()
	isEmpty() // return true
####Tags Expand
Stack Queue

####思路
- 这个题没有实际意义,就是练练手

```java
class Stack {
    // Push a new item into the stack
    private Queue<Integer> queue1 = new LinkedList<Integer>();
    private Queue<Integer> queue2 = new LinkedList<Integer>();
    private int count = 0;

    public void push(int x) {
        // Write your code here
        if (queue1.isEmpty()) {
            queue2.offer(x);
        } else if(queue2.isEmpty()) {
            queue1.offer(x);
        }
        count++;
    }

    // Pop the top of the stack
    public void pop() {
        // Write your code here
        int popnumber = count - 1;
        if (queue1.isEmpty()) {
            while (popnumber > 0) {
                queue1.offer(queue2.poll());
                popnumber--;
            }
            queue2.poll();
        } else if (queue2.isEmpty()) {
            while (popnumber > 0) {
                queue2.offer(queue1.poll());
                popnumber--;
            }
            queue1.poll();
        }
        count--;
    }

    // Return the top of the stack
    public int top() {
        // Write your code here
        int popnumber = count - 1;
        int result = 0;
        if (queue1.isEmpty()) {
            while (popnumber > 0) {
                queue1.offer(queue2.poll());
                popnumber--;
            }
            result = queue2.peek();
            queue1.offer(queue2.poll());
        } else if (queue2.isEmpty()) {
            while (popnumber > 0) {
                queue2.offer(queue1.poll());
                popnumber--;
            }
            result = queue1.peek();
            queue2.offer(queue1.poll());
        }
        return result;
    }

    // Check the stack is empty or not.
    public boolean isEmpty() {
        // Write your code here
        return queue1.isEmpty() && queue2.isEmpty();
    }
}
```
