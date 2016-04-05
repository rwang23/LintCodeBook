##Perfect Squares

	Total Accepted: 30400 Total Submissions: 94448 Difficulty: Medium
	Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

	For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.

####思路
- 有三种思路[参考](https://leetcode.com/discuss/58056/summary-of-different-solutions-bfs-static-and-mathematics)

####动规方法
- 设置dp[i] 为第i个数需要的perfect square numbers
- dp[i] = Math.min(d[i - j * j] + 1, dp[i])
- dp[0] = 0, 其他都是最大值

```java
public class Solution {
    public int numSquares(int n) {
        if (n <= 0) {
            return -1;
        }
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;
        for (int i = 1; i <= n; i++) {
            int min = Integer.MAX_VALUE;
            int j = 1;
            while(i - j*j >= 0) {
                min = Math.min(min, dp[i - j*j] + 1);
                j++;
            }
            dp[i] = min;
        }
        return dp[n];
    }
}
```

####数学方法
- [参考](http://www.cnblogs.com/grandyang/p/4800552.html)
- 考察四平方和定理
- 根据四平方和定理，任意一个正整数均可表示为4个整数的平方和，其实是可以表示为4个以内的平方数之和，那么就是说返回结果只有1,2,3或4其中的一个


####结合dp和数学
```java
public class Solution {
    public int numSquares(int n) {
        if (n <= 0) {
            return -1;
        }
        while (n % 4 == 0) {
            n /= 4;
        }
        if (n % 8 == 7) return 4;

        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for (int i = 1; i <= n; i++) {
            int min = Integer.MAX_VALUE;
            int j = 1;
            while(i - j*j >= 0) {
                min = Math.min(min, dp[i - j*j] + 1);
                j++;
            }
            dp[i] = min;
        }
        return dp[n];
    }
}
```
