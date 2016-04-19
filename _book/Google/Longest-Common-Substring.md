##Longest Common Substring

30% Accepted

	Given two strings, find the longest common substring.

	Return the length of it.

	Have you met this question in a real interview? Yes
	Example
	Given A = "ABCD", B = "CBCE", return 2.

	Note
	The characters in substring should occur continuously in original string. This is different with subsequence.

####Challenge
- O(n x m) time and memory.

####Tags Expand
- LintCode Copyright
- Longest Common Subsequence
- Dynamic Programming

####思路
- 此题跟Longest Common Subsequence不一样，是求substring
- 还是画图看
- 如果不再相等，该辅助点就应该置零
- 最后找辅助矩阵中最大点 就是最大长度


```java
public class Solution {
    /**
     * @param A, B: Two string.
     * @return: the length of the longest common substring.
     */
    public int longestCommonSubstring(String A, String B) {
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
        int max = 0;
        for (int i = 1; i <= A.length(); i++) {
            for (int j = 1; j <= B.length(); j++) {
                lcs[i][j] = 0;
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    lcs[i][j] = lcs[i - 1][j - 1] + 1;
                    max = Math.max(max, lcs[i][j]);
                }

            }
        }
        return max;
    }
}

```
