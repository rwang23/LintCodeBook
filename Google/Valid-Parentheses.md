##Valid Parentheses

27% Accepted

	Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

	Have you met this question in a real interview? Yes
	Example
	The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

####Tags Expand
- Stack


```java
public class Solution {
    /**
     * @param s A string
     * @return whether the string is a valid parentheses
     */
    public boolean isValidParentheses(String s) {
        // Write your code here
        if (s == null) {
            return true;
        }
        if (s.length() % 2 == 1) {
            return false;
        }
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < s.length(); i++) {
            char thisChar = s.charAt(i);
            if (thisChar == '(' || thisChar == '{' || thisChar == '[') {
                stack.push(thisChar);
            } else {
                if ((thisChar == ')' && stack.pop() != '(') || (thisChar == '}' && stack.pop() != '{') || (thisChar == ']' && stack.pop() != '[')) {
                    return false;
                }
            }
        }
        if (stack.isEmpty()) {
            return true;
        }
        return false;
    }
}

```
####稍微简化的写法，使用Hashmap
```java
public static boolean isValidParentheses(String s) {
	HashMap<Character, Character> map = new HashMap<Character, Character>();
	map.put('(', ')');
	map.put('[', ']');
	map.put('{', '}');

	Stack<Character> stack = new Stack<Character>();

	for (int i = 0; i < s.length(); i++) {
		char curr = s.charAt(i);

		if (map.keySet().contains(curr)) {
			stack.push(curr);
		} else if (map.values().contains(curr)) {
			if (!stack.empty() && map.get(stack.peek()) == curr) {
				stack.pop();
			} else {
				return false;
			}
		}
	}

	return stack.empty();
}
```
