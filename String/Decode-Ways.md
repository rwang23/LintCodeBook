##Decode Ways

Total Accepted: 66183 Total Submissions: 379749 Difficulty: Medium
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.

####思路
- 动规,思路不难想到
- 但是是从1开始的,所以对0的处理就很重要了
- 会有10 20,满足规则但是30 40不行
- 同时21 22可以,但是27 28不能
- 也不能31 32

```java
public class Solution {
    /*
    state:
    dp[i], how many num of decodings of first i char
    function:
    if (char(i - 2) == 1 || == 2)
    dp[i] = dp[i - 1] + dp[i - 2]
    else
    dp[i] = dp[i - 1]
    initialize:
    dp[0] = 1;
    if (char(0) == 1 || == 2)
    dp[1] = 2
    else
    dp[1] = 1
    answer:
    dp[size - 1]

    */
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int size = s.length();
        if (s.charAt(0) == '0') {
            return 0;
        }
        if (size == 1) {
            return 1;
        }
        int[] dp = new int[size];

        dp[0] = 1;
        dp[1] = ((s.charAt(0) == '1') || (s.charAt(0) == '2' && s.charAt(1) <= '6')) ? 2 : 1;
        if (s.charAt(1) == '0') {
            if (s.charAt(0) == '1' || s.charAt(0) == '2') {
                dp[1] = 1;
            } else {
                return 0;
            }
        }

        for (int i = 2; i < size; i++) {
            if (s.charAt(i) == '0' && (s.charAt(i - 1) != '1' && s.charAt(i - 1) != '2')) {
                return 0;
            } else {
                if (s.charAt(i) == '0') {
                    dp[i] = dp[i - 2];
                }
                // if (s.charAt(i - 1) == '0') {
                //     dp[i] = dp[i - 1];
                // }
                else if ((s.charAt(i - 1) == '1') || (s.charAt(i - 1) == '2' && s.charAt(i) <= '6')) {
                    dp[i] = dp[i - 1] + dp[i - 2];
                }
                else {
                    dp[i] = dp[i - 1];
                }
            }
        }

        return dp[size - 1];
    }
}
```

####空间优化

```java
public class Solution {
    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int size = s.length();
        if (s.charAt(0) == '0') {
            return 0;
        }
        if (size == 1) {
            return 1;
        }
        int[] dp = new int[3];

        dp[0] = 1;
        dp[1] = ((s.charAt(0) == '1') || (s.charAt(0) == '2' && s.charAt(1) <= '6')) ? 2 : 1;
        if (s.charAt(1) == '0') {
            if (s.charAt(0) == '1' || s.charAt(0) == '2') {
                dp[1] = 1;
            } else {
                return 0;
            }
        }

        for (int i = 2; i < size; i++) {
            if (s.charAt(i) == '0' && (s.charAt(i - 1) != '1' && s.charAt(i - 1) != '2')) {
                return 0;
            } else {
                if (s.charAt(i) == '0') {
                    dp[i % 3] = dp[(i - 2) % 3];
                }
                else if ((s.charAt(i - 1) == '1') || (s.charAt(i - 1) == '2' && s.charAt(i) <= '6')) {
                    dp[i % 3] = dp[(i - 1) % 3] + dp[(i - 2) % 3];
                }
                else {
                    dp[i % 3] = dp[(i - 1) % 3];
                }
            }
        }

        return dp[(size - 1) % 3];
    }
}
```
