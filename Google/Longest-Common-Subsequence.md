##Longest Common Subsequence

37% Accepted

	Given two strings, find the longest common subsequence (LCS).

	Your code should return the length of LCS.

	Have you met this question in a real interview? Yes
	Example
	For "ABCD" and "EDCA", the LCS is "A" (or "D", "C"), return 1.

	For "ABCD" and "EACB", the LCS is "AC", return 2.

	Clarification
	What's the definition of Longest Common Subsequence?

####Related Information
- https://en.wikipedia.org/wiki/Longest_common_subsequence_problem
- http://baike.baidu.com/view/2020307.htm

####Tags Expand
- LintCode Copyright
- Longest Common Subsequence
- Dynamic Programming

####思路
- Two sequence DP
- 画图 找规律： 一定存在lcs[i][j] 与lcs[i-1][j],lcs[i][j-1 ],lcs[i-][j-1]的关系
- 初始化也很重要
- java中，int数组如果没有赋初始值，那么就是0，在本题中，单独列出初始化
- 依次动态查找，不存在顺序问题，找到就加一，这个跟Longest Common Substring不一样

```java
public class Solution {
    /**
     * @param A, B: Two strings.
     * @return: The length of longest common subsequence of A and B.
     */
    public int longestCommonSubsequence(String A, String B) {
        // write your code here
        if (A == null || B == null) {
            return 0;
        }
        int[][] lcs = new int[A.length() + 1][B.length() + 1];
        for (int i = 0; i<= A.length(); i++) {
            lcs[i][0] = 0;
        }
        for (int i = 0; i<= B.length(); i++) {
            lcs[0][i] = 0;
        }
        for (int i = 1; i <= A.length(); i++) {
            for (int j = 1; j <= B.length(); j++) {
                lcs[i][j] = Math.max(lcs[i - 1][j], lcs[i][j - 1]);
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    lcs[i][j] = lcs[i - 1][j - 1] + 1;
                }

            }
        }

        return lcs[A.length()][B.length()];
    }
}


```
