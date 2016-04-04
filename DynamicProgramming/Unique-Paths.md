##Unique Paths

    35% Accepted

	A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

	The robot can only move either down or right at any point in time.
    The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

	How many possible unique paths are there?

####Note
- m and n will be at most 100.

####Tags Expand
- Dynamic Programming
- Array

####思路
- 这道题跟minimum path sum基本一样，无非就是换了初始化

```java
public class Solution {
    /**
     * @param n, m: positive integer (1 <= n ,m <= 100)
     * @return an integer
     */
    public int uniquePaths(int m, int n) {
        // write your code here

        int[][] sum = new int[m][n];
        for (int i = 0; i < m; i++) {
            sum[i][0] = 1;
        }
        for (int i = 0; i < n; i++) {
            sum[0][i] = 1;
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j< n; j++) {
                sum[i][j] = sum[i-1][j] + sum[i][j-1];
            }
        }
        return sum[m-1][n-1];
    }
}
```

####空间优化
```java
public class Solution {
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[2][n];

        for (int i = 0; i < n; i++) {
            dp[0][i] = 1;
        }

        for (int i = 1; i < m; i++) {
            dp[i % 2][0] = 1;
            for (int j = 1; j < n; j++) {
                dp[i % 2][j] = dp[(i - 1) % 2][j] + dp[i % 2][j - 1];
            }
        }
        return dp[(m - 1) % 2][n - 1];
    }
}
```
