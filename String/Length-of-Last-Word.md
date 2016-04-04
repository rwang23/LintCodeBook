##Length of Last Word

	Total Accepted: 88656 Total Submissions: 304501 Difficulty: Easy
	Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

	If the last word does not exist, return 0.

	Note: A word is defined as a character sequence consists of non-space characters only.

	For example,
	Given s = "Hello World",
	return 5.

##思路
- 可能会被问到trim如何实现,很简单,遍历一遍,找到最后有字符的地方

```java
public class Solution {
    public int lengthOfLastWord(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        s = s.trim();
        int pre = -1;
        int len = s.length();
        for (int i = 0; i < len; i++) {
            if (s.charAt(i) == ' ') {
                pre = i;
            }
        }

        return (len - 1) - pre;
    }
}
```
