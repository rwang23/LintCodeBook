##Longest Common Prefix

	Total Accepted: 94243 Total Submissions: 337613 Difficulty: Easy
	Write a function to find the longest common prefix string amongst an array of strings.

####思路
- 直接做,因为无论如何也要O(kn),n是string的数量,k是common prefix长度

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return new String();
        }
        StringBuilder string = new StringBuilder();
        int size = strs.length;
        for (int i = 0; i < strs[0].length(); i++) {
            char cur = strs[0].charAt(i);
            for (int j = 1; j < size; j++) {
                String s = strs[j];
                if (i >= s.length() || s.charAt(i) != cur) {
                    return string.toString();
                }
            }
            string.append(cur);
        }
        return string.toString();
    }
}
```
