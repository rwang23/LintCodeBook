##Word Pattern
	Total Accepted: 34543 Total Submissions: 118751 Difficulty: Easy
	Given a pattern and a string str, find if str follows the same pattern.

	Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

	Examples:
	pattern = "abba", str = "dog cat cat dog" should return true.
	pattern = "abba", str = "dog cat cat fish" should return false.
	pattern = "aaaa", str = "dog cat cat dog" should return false.
	pattern = "abba", str = "dog dog dog dog" should return false.
	Notes:
	You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

####思路
- hashmap

```java
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        if (pattern == null && str == null) {
            return true;
        }

        if (pattern == null || str == null) {
            return false;
        }

        String[] strings = str.split(" ");
        char[] chars = pattern.toCharArray();

        if (strings.length != chars.length) {
            return false;
        }

        Map<Character, String> map = new HashMap<Character, String>();
        Set<String> set = new HashSet<String>();

        for (int i = 0; i < strings.length; i++) {
            String curString = strings[i];
            char curChar = chars[i];

            if (map.containsKey(curChar)) {
                if (!map.get(curChar).equals(curString)) {
                    return false;
                }
            } else {
                if (set.contains(curString)) {
                    return false;
                }
                map.put(curChar, curString);
                set.add(curString);
            }
        }
        return true;
    }
}
```
