##Wildcard Matching
	Total Accepted: 55214 Total Submissions: 317630 Difficulty: Hard
	Implement wildcard pattern matching with support for '?' and '*'.

	'?' Matches any single character.
	'*' Matches any sequence of characters (including the empty sequence).

	The matching should cover the entire input string (not partial).

	The function prototype should be:
	bool isMatch(const char *s, const char *p)

	Some examples:
	isMatch("aa","a") → false
	isMatch("aa","aa") → true
	isMatch("aaa","aa") → false
	isMatch("aa", "*") → true
	isMatch("aa", "a*") → true
	isMatch("ab", "?*") → true
	isMatch("aab", "c*a*b") → false

####思路
- 与regular expression matching相类似
- 找dp的规律就可以
- 主要注意的是初始化,可能会遇到"" 与 "**"对应的情况
- 0(n2)

```java
/*
state: dp[i][j] means first i char from s can match first j char from p
function:
if schar = pchar or pchar == '?'  then dp[i][j] = dp[i - 1][j - 1]
if pchar == '*' then dp[i][j] = dp[i][j - 1] || dp[i - 1][j]
initialize: dp[0][i] = dp[i][0] = false, dp[0][0] = true
answer : dp[m][n], m = s.length() n = p.length()
*/

public class Solution {
    public boolean isMatch(String s, String p) {
        if ((s == null && p == null) || (s.equals("") && p.equals(""))) {
            return true;
        }
        if ((s == null || p == null || p.equals(""))) {
            return false;
        }
        int m = s.length();
        int n = p.length();

        boolean[][] dp = new boolean[m + 1][n + 1];
        dp[0][0] = true;
        int x = 0;
        while (x < n && p.charAt(x) == '*') {
            for (int i = 0; i <= m; i++) {
                dp[i][x + 1] = true;
            }
            x++;
        }

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                char schar = s.charAt(i - 1);
                char pchar = p.charAt(j - 1);
                if (schar == pchar || pchar == '?') {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                if (pchar == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                }
            }
        }

        return dp[m][n];
    }
}
```
