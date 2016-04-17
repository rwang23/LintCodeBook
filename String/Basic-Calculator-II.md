##Basic Calculator II

	Total Accepted: 20498 Total Submissions: 82974 Difficulty: Medium
	Implement a basic calculator to evaluate a simple expression string.

	The expression string contains only non-negative integers, +, -, *, / operators and empty spaces.
    The integer division should truncate toward zero.

	You may assume that the given expression is always valid.

	Some examples:
	"3+2*2" = 7
	" 3/2 " = 1
	" 3+5 / 2 " = 5
	Note: Do not use the eval built-in library function.

####思路
- 用stack 不断push进取
- 当时-时,就是Push -num

```java
public class Solution {
    public int calculate(String s) {
        int len;
        if (s==null || (len = s.length())==0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<Integer>();
        int num = 0;
        char sign = '+';
        for (int i=0;i<len;i++) {
            if (Character.isDigit(s.charAt(i))) {
                num = num*10+s.charAt(i)-'0';
            }
            if ((!Character.isDigit(s.charAt(i)) &&' '!=s.charAt(i)) || i==len-1) {
                if (sign=='-') {
                    stack.push(-num);
                }
                if (sign=='+') {
                    stack.push(num);
                }
                if (sign=='*') {
                    stack.push(stack.pop()*num);
                }
                if (sign=='/') {
                    stack.push(stack.pop()/num);
                }
                sign = s.charAt(i);
                num = 0;
            }
        }

        int re = 0;
        for (int i:stack) {
            re += i;
        }
        return re;
    }
}
```
