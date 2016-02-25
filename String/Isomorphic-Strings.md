##Isomorphic Strings

	Given two strings s and t, determine if they are isomorphic.

	Two strings are isomorphic if the characters in s can be replaced to get t.

	All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

	For example,
	Given "egg", "add", return true.

	Given "foo", "bar", return false.

	Given "paper", "title", return true.

	Note:
	You may assume both s and t have the same length.

####思路
- 寻找string pattern
- 用了hashmap来存

```java
public class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s == null && t == null) {
            return true;
        }
        if (s == null || t == null) {
            return false;
        }
        if (s.length() != t.length()) {
            return false;
        }
        HashMap<Character, Character> map1 = new HashMap<Character, Character>();
        HashMap<Character, Character> map2 = new HashMap<Character, Character>();

        for (int i = 0; i < s.length(); i++) {
            char sChar = s.charAt(i);
            char tChar = t.charAt(i);

            if (!map1.containsKey(sChar)) {
                map1.put(sChar, tChar);
            } else {
                if (map1.get(sChar) != tChar) {
                    return false;
                }
            }

            if (!map2.containsKey(tChar)) {
                map2.put(tChar, sChar);
            } else {
                if (map2.get(tChar) != sChar) {
                    return false;
                }
            }

        }
        return true;
    }
}
```
