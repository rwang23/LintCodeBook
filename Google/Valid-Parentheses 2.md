##Valid Parentheses
	Total Accepted: 103841 Total Submissions: 354982 Difficulty: Easy
	Given a string containing just the characters '(', ')', '{', '}', '[' and ']',
	determine if the input string is valid.

	The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

####思路
- stack

```java
public class Solution {
    /*
    ([{adf}])
    ([sad]))
    */
    public boolean isValid(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        Stack<Character> stack = new Stack<Character>();
        Map<Character, Character> map = new HashMap<Character, Character>();

        map.put('(', ')');
        map.put('[', ']');
        map.put('{', '}');

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (map.containsKey(c)) {
                stack.push(c);
            } else {
                if (c == ')' || c == ']' || c == '}') {
                    if (stack.isEmpty()) {
                        return false;
                    }
                    char original = stack.pop();
                    if (map.get(original) != c) {
                        return false;
                    }
                }
            }
        }
        return stack.size() == 0 ? true : false;

        /*
        (((((
        */
    }
}
```
