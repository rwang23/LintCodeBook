##Reverse Words in a String II

	Total Accepted: 9061 Total Submissions: 31060 Difficulty: Medium
	Given an input string, reverse the string word by word.
	A word is defined as a sequence of non-space characters.

	The input string does not contain leading or trailing spaces and the words are always separated by a single space.

	For example,
	Given s = "the sky is blue",
	return "blue is sky the".

	Could you do it in-place without allocating extra space?

####思路
- 三步翻转

```java
public class Solution {
    public void reverseWords(char[] s) {
        if (s == null || s.length == 0) {
            return;
        }
        int len = s.length;
        reverse(s, 0, len - 1);
        int pre = 0;
        for (int i = 0; i < len; i++) {
            if (s[i] == ' ') {
                reverse(s, pre, i - 1);
                pre = i + 1;
            }
        }

        reverse(s, pre, len - 1);
    }

    public void reverse(char[] s, int start, int end) {

        while (start < end) {
            char temp = s[start];
            s[start] = s[end];
            s[end] = temp;
            start++;
            end--;
        }
    }
}
```
