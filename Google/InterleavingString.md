##Interleaving String

26% Accepted

	Given three strings: s1, s2, s3, determine whether s3 is formed by the interleaving of s1 and s2.

	Have you met this question in a real interview? Yes
	Example
	For s1 = "aabcc", s2 = "dbbca"

	When s3 = "aadbbcbcac", return true.
	When s3 = "aadbbbaccc", return false.

####Challenge
- O(n2) time or better

####Tags Expand
- Longest Common Subsequence
- Dynamic Programming

####思路
- 见代码注释

```java
public class Solution {
    /**
     * Determine whether s3 is formed by interleaving of s1 and s2.
     * @param s1, s2, s3: As description.
     * @return: true or false.
     */
     //state: ret[i][j] 是s1前i个字符与s2前j个字符能否构成s1的前i+j个字符
     //function: 还是通过最后一位是否相同来切入
     //initialize: ret[i][0]=true ret[0][j]=true是错误的有问题的，有可能s3本来就不是s1 s2生成的，所以在初始化的时候就要判断好
     //answer: ret[n+1][m+1]
    public boolean isInterleave(String s1, String s2, String s3) {
        // write your code here
        if (s1.length() + s2.length() != s3.length()) {
            return false;
        }
        boolean[][] ret = new boolean[s1.length() + 1][s2.length() + 1];
        ret[0][0] = true;
        for (int i = 1; i <= s1.length(); i++) {
            if (s3.charAt(i - 1) == s1.charAt(i - 1) && ret[i - 1][0]) {
                ret[i][0] = true;
            } else {
                ret[i][0] = false;
            }
        }
        for (int j = 1; j <= s2.length(); j++) {
            if (s3.charAt(j - 1) == s2.charAt(j - 1) && ret[0][j - 1]) {
                ret[0][j] = true;
            } else {
                ret[0][j] = false;
            }
        }
        for (int i = 1; i <= s1.length(); i++) {
            for (int j = 1; j <= s2.length(); j++) {
                //为什么要把ret[i][j-1]写在条件里边呢？
                //因为如果是这么写ret[i][j] = ret[i][j-1],有可能末位只是凑巧相等
                //s1 s2 末位字符是一样的，所以加上ret[i][j-1]去判断
                if (s3.charAt(i + j - 1) == s2.charAt(j - 1) && ret[i][j - 1]) {
                    ret[i][j] = true;
                } else if (s3.charAt(i + j - 1) == s1.charAt(i - 1) && ret[i - 1][j]) {
                    ret[i][j] = true;
                } else {
                    ret[i][j] = false;
                }
            }
        }
        return ret[s1.length()][s2.length()];
    }
}

```
