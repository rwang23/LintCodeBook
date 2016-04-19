##Stack Sorting

	Sort a stack in ascending order (with biggest terms on top).

	You may use at most one additional stack to hold items,
	but you may not copy the elements into any other data structure (e.g. array).

	Example
	Given stack =

	| |
	|3|
	|1|
	|2|
	|4|
	 -
	return:

	| |
	|4|
	|3|
	|2|
	|1|
	 -
	The data will be serialized to [4,2,1,3]. The last element is the element on the top of the stack.

####Challenge
O(n^2) time is acceptable.

####Tags Expand
Stack

####思路
- 两个stack
- 先遍历一遍放在stack2里边,求出stack长度(好像可以直接用size()),不过这一步先找出最大值
- 然后记录下最大值,把其他的push到另外一个stack,再把最大值push到此个已经空的stack
- 下一轮push的时候,就设定一个总共push的数量,使得刚好不把这个最大值push了,
- 同时此轮也将次大值放了进来
- 其中一个易错点是, 如果stack里边有多个数值一样的值,那么这些值都是最大值,都不push到另一个里面,而且都Push到这个放最大值的stack里边


```java
public class Solution {
    /**
     * @param stack an integer stack
     * @return void
     */
    public void stackSorting(Stack<Integer> stack) {
        // Write your code here
        if (stack.isEmpty()) {
            return;
        }
        Stack<Integer> stack2 = new Stack<Integer>();
        int size = 0;
        int max = Integer.MIN_VALUE;
        while (!stack.isEmpty()) {
            int cur = stack.pop();
            stack2.push(cur);
            size++;
            max = Math.max(max, cur);
        }

        int instack = 0;
        for (int i = 0; i < size ; i++) {
            int samenumber = 0;
            for (int j = 0; j < size - instack; j++) {
                int cur = stack2.pop();
                if (cur != max) {
                    stack.push(cur);
                }
                if (cur == max) {
                    samenumber++;
                }
            }
            for (int j = 0; j < samenumber; j++) {
                stack2.push(max);
            }
            max = Integer.MIN_VALUE;
            for (int j = 0; j < size - samenumber - instack; j++) {
                int cur = stack.pop();
                max = Math.max(max, cur);
                stack2.push(cur);
            }
            instack = instack + samenumber;
        }

        while (!stack2.isEmpty()) {
            stack.push(stack2.pop());
        }
    }
}
```
