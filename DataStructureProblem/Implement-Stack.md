##Implement Stack

	Implement a stack.
	You can use any data structure inside a stack except stack itself to implement it.

	Have you met this question in a real interview? Yes
	Example
	push(1)
	pop()
	push(2)
	top()  // return 2
	pop()
	isEmpty() // return true
	push(3)
	isEmpty() // return false

####Tags Expand
Array Stack

####思路

```java
class Stack {
    // Push a new item into the stack
    private ListNode head = null;

    private class ListNode {
        int val;
        ListNode next;
        ListNode(int x) {
            this.val = x;
            this.next = null;
        }
    }
    public void push(int x) {
        // Write your code here
        if (head == null) {
            head = new ListNode(x);
        } else {
            ListNode newhead = new ListNode(x);
            newhead.next = head;
            head = newhead;
        }
    }

    // Pop the top of the stack
    public void pop() {
        // Write your code here
        if (head != null) {
            head = head.next;
        }
    }

    // Return the top of the stack
    public int top() {
        // Write your code here
        return head.val;
    }

    // Check the stack is empty or not.
    public boolean isEmpty() {
        // Write your code here
        return head == null;
    }
}
```
