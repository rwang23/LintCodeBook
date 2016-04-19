##Letter Combinations of a Phone Number

22% Accepted

[题目有图片](http://www.lintcode.com/en/problem/letter-combinations-of-a-phone-number/)

	Given a digit string, return all possible letter combinations that the number could represent.

	A mapping of digit to letters (just like on the telephone buttons) is given below.

	Cellphone

	Have you met this question in a real interview? Yes
	Example
	Given "23"

	Return ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]

####Note
	Although the above answer is in lexicographical order,
	your answer could be in any order you want.

####Tags Expand
- String
- Backtracking
- Recursion


####思路
- 典型DFS
- 值得注意的是,这个combination不是把所有字母合在一起,而是比如"23",从2的字母取一个,3的取一个
- char c : map.get(digits.charAt(sb.length())) 这个写法值得掌握

```java
public class Solution {
    public ArrayList<String> letterCombinations(String digits) {
        ArrayList<String> result = new ArrayList<String>();

        if (digits == null || digits.equals("")) {
            return result;
        }

        Map<Character, char[]> map = new HashMap<Character, char[]>();
        map.put('0', new char[] {});
        map.put('1', new char[] {});
        map.put('2', new char[] { 'a', 'b', 'c' });
        map.put('3', new char[] { 'd', 'e', 'f' });
        map.put('4', new char[] { 'g', 'h', 'i' });
        map.put('5', new char[] { 'j', 'k', 'l' });
        map.put('6', new char[] { 'm', 'n', 'o' });
        map.put('7', new char[] { 'p', 'q', 'r', 's' });
        map.put('8', new char[] { 't', 'u', 'v'});
        map.put('9', new char[] { 'w', 'x', 'y', 'z' });

        StringBuilder sb = new StringBuilder();
        helper(map, digits, sb, result);

        return result;
    }

    private void helper(Map<Character, char[]> map, String digits,
        StringBuilder sb, ArrayList<String> result) {
        if (sb.length() == digits.length()) {
            result.add(sb.toString());
            return;
        }

        for (char c : map.get(digits.charAt(sb.length()))) {
            sb.append(c);
            helper(map, digits, sb, result);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
