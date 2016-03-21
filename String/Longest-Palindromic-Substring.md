##Longest Palindromic Substring

	Total Accepted: 99803 Total Submissions: 438290 Difficulty: Medium
	Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring


####思路
- 区间型动态规划O(n2)
- Manacher O(n)但是不用去刻意掌握
- 使用substring这个函数其实是O(n)时间复杂度,所以不要直接用,而是记录下Index就好了

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return new String();
        }

        int size = s.length();
        boolean[][] dp = new boolean[size][size];
        String longest = new String();
        int start = 0;
        int end = size - 1;

        for (int i = 0; i < size; i++) {
            dp[i][i] = true;
        }

        for (int i = 0; i + 1< size; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                start = i;
                end = i + 1;
            }
        }

        for (int len = 2; len < size; len++) {
            for (int i = 0; i + len < size; i++) {
                if (s.charAt(i) == s.charAt(i + len) && dp[i + 1][i + len - 1]) {
                    dp[i][i + len] = true;
                    start = i;
                    end = i + len;
                }
            }
        }
        longest = s.substring(start, end + 1);

        return longest;
    }
}
```
