##Basic Calculator
	Total Accepted: 26713 Total Submissions: 121377 Difficulty: Hard
	Implement a basic calculator to evaluate a simple expression string.

	The expression string may contain open ( and closing parentheses ), the plus + or minus sign -, non-negative integers and empty spaces .

	You may assume that the given expression is always valid.

	Some examples:
	"1 + 1" = 2
	" 2-1 + 2 " = 3
	"(1+(4+5+2)-3)+(6+8)" = 23
	Note: Do not use the eval built-in library function.

####思路
- 不难,但是还挺容易错误的
- 参考[图文解释](http://yucoding.blogspot.com/2015/10/leetcode-question-basic-calculator.html)
- 最直观的想法就是一个stack存数字,一个stack 存 () +-这些符号
- 解法用存入同一个stack 1, -1 来模拟了加减

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> stackInt = new Stack<>();
        stackSign = new Stack<>();
        int result = 0;
        int sign = 1;
        int num = 0;
        for(int i=0; i<s.length(); i++) {
            char c = s.charAt(i);
            if(c >= '0' && c <= '9') {
                int digit = Character.getNumericValue(c);
                num = 10 * num + digit;
            } else if(c == '+' || c == '-') {
                result += num * sign;
                num = 0;
                sign = c == '+' ? 1 : -1;
            } else if(c == '(') {
                stackInt.push(result);
                stackSign.push(sign);
                result = 0;
                sign = 1;
            } else if(c == ')') {
                result += num * sign;
                result = result * stackSign.pop() + stackInt.pop();
                num = 0;
                sign = 1;
            }
        }
        result += num * sign;
        return result;
    }

}
```
