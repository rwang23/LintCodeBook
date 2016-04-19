##Min Stack

30% Accepted

	Implement a stack with min() function, which will return the smallest number in the stack.

	It should support push, pop and min operation all in O(1) cost.

	Have you met this question in a real interview? Yes
	Example
	push(1)
	pop()   // return 1
	push(2)
	push(3)
	min()   // return 2
	push(1)
	min()   // return 1
	Note
	min operation will never be called if there is no number in the stack.

####Tags Expand
- Stack

####思路
- 设置两个stack,一个存正常值，一个存最小值
- 存最小值的时候，每次存的是当前的最小值

```java
public class MinStack {
    private Stack<Integer> stack1;
    private Stack<Integer> stack2;
    private int min;

    public MinStack() {
        // do initialize if necessary
        stack1 = new Stack<Integer>();
        stack2 = new Stack<Integer>();
        min = Integer.MAX_VALUE;
    }

    public void push(int number) {
        // write your code here
        stack1.push(number);
        if (number < min) {
            min = number;
        }
        stack2.push(min);
    }

    public int pop() {
        // write your code here
        int x = stack2.pop();
        int y = stack1.pop();
        if (stack2.isEmpty()) {
            min = Integer.MAX_VALUE;
        } else {
            min = stack2.peek();
        }
        return y;
    }

    public int min() {
        // write your code here
        return stack2.peek();
    }
}


```
