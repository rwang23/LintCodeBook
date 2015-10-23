##Distinct Subsequences

30% Accepted

	Given a string S and a string T, count the number of distinct subsequences of T in S.

	A subsequence of a string is a new string
    which is formed from the original string by deleting some (can be none) of the characters
    without disturbing the relative positions of the remaining characters.
    (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).

	Have you met this question in a real interview? Yes
	Example
	Given S = "rabbbit", T = "rabbit", return 3.

####Challenge
- Do it in O(n2) time and O(n) memory.
- O(n2) memory is also acceptable if you do not know how to optimize memory.

####Tags Expand
- String
- Dynamic Programming


----

####O(n2) memory 思路
- Two Sequence DP
- 仔细理解题意，题目意思不是很明确
- 画图找规律，直接看不到规律就自己凑规律，其实都是数学原理
- 画出矩阵型的图去找规律匹配

####题意理解

	Since you can choose two b from three and there are total of 3 choices, i.e.,

	the first and the second
	the first and the third
	the second and the third

```java
public class Solution {
    /**
     * @param S, T: Two string.
     * @return: Count the number of distinct subsequences
     */
    public int numDistinct(String S, String T) {
        // write your code here
        int[][] ret = new int[S.length()+1][T.length()+1];
        for (int i = 0 ; i <= T.length(); i++) {
            ret[0][i] = 0;
        }
        for (int i = 0 ; i <= S.length(); i++) {
            ret[i][0] = 1;
        }
        for (int i = 1; i <= S.length(); i++) {
            for (int j = 1; j <= T.length(); j++) {
                if (i < j) {
                    ret[i][j] = 0;
                    continue;
                }
                if (S.charAt(i - 1) != T.charAt(j - 1)) {
                    ret[i][j] = ret[i - 1][j];
                } else {
                    ret[i][j] = ret[i-1][j-1] + ret[i-1][j];
                }
            }
        }

        return ret[S.length()][T.length()];
    }
}

```
####O(n) memory 思路
- [来自Yu's Garden 第四种解法](http://www.cnblogs.com/yuzhangcmu/p/4196373.html)
