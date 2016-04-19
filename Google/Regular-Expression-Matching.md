##Regular Expression Matching

	Total Accepted: 77341 Total Submissions: 352914 Difficulty: Hard
	Implement regular expression matching with support for '.' and '*'.

	'.' Matches any single character.
	'*' Matches zero or more of the preceding element.

	The matching should cover the entire input string (not partial).

	The function prototype should be:
	bool isMatch(const char *s, const char *p)

	Some examples:
	isMatch("aa","a") → false
	isMatch("aa","aa") → true
	isMatch("aaa","aa") → false
	isMatch("aa", "a*") → true
	isMatch("aa", ".*") → true
	isMatch("ab", ".*") → true
	isMatch("aab", "c*a*b") → true

####思路
- 使用了动规
- dp[i][j],s的前i个字符能否匹配p的前j个字符
- if schar == pchar or pchar == '.' then dp[i][j] = dp[i - 1][j - 1];
- if pchar = * 因为*代表了零个前边字符或者多个,所以
- 当代表零个的时候 dp[i][j] = dp[i][j - 1]
- 当代表一个的时候 dp[i][j] = dp[i][j - 2]
- 当代表多个的时候,同时此时schar等于它的前一个字符 dp[i][j] = dp[i - 1][j]
- 同时在初始化的时候,并不是dp[0][i] = false, dp[i][0] = false
- 比如"" 跟 "d*" 匹配,他俩是匹配的,dp[0][2] = true
- 所以初始化的时候, pchar = *, dp[0][i] = dp[0][i - 1] || dp[0][i - 2];


```java
public class Solution {
    public boolean isMatch(String s, String p) {
        if (s == null && p == null) {
            return true;
        }

        if (s == null || p == null) {
            return false;
        }

        int m = s.length();
        int n = p.length();
        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;

        for (int i = 2; i <= n; i++) {
            char pchar = p.charAt(i - 1);
            if (pchar == '*') {
                dp[0][i] = dp[0][i - 1] || dp[0][i - 2];
            }
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char schar = s.charAt(i - 1);
                char pchar = p.charAt(j - 1);
                if (schar == pchar || pchar == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                }

                if (pchar == '*') {
                    if (j >= 2) {
                        if (schar == p.charAt(j - 2) || p.charAt(j - 2) == '.') {
                            dp[i][j] = dp[i][j - 1] || dp[i - 1][j] || dp[i][j - 2];
                        } else {
                            dp[i][j] = dp[i][j - 1] || dp[i][j - 2];
                        }
                    }
                }
            }
        }

        return dp[m][n];
    }
}
```
