##Longest Increasing Path in a Matrix

    Difficulty: Medium
    Given an integer matrix, find the length of the longest increasing path.

    From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

    Example 1:

    nums = [
      [9,9,4],
      [6,6,8],
      [2,1,1]
    ]
    Return 4
    The longest increasing path is [1, 2, 6, 9].

    Example 2:

    nums = [
      [3,4,5],
      [3,2,6],
      [2,2,1]
    ]
    Return 4
    The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed

####思路
- 如下的直接动规是错误的
- 这道题属于记忆化搜索

```java
public class Solution {
    public int longestIncreasingPath(int[][] matrix) {
        int m = matrix.length;
        if (m == 0) {
            return -1;
        }
        int n = matrix[0].length;
        if (n == 0) {
            return -1;
        }

        int[][] dp = new int[m][n];
        dp[0][0] = 1;
        int max = 0;
        for (int j = 1; j < n; j++) {
            if (matrix[0][j] >= matrix[0][j - 1]) {
                dp[0][j] = dp[0][j - 1] + 1;
            } else {
                dp[0][j] = 1;
            }
            max = Math.max(max, dp[0][j]);
        }

        for (int i = 1; i < m; i++) {
            if (matrix[i][0] >= matrix[i - 1][0]) {
                dp[i][0] = dp[i - 1][0] + 1;
            } else {
                dp[i][0] = 1;
            }
             max = Math.max(max, dp[i][0]);
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = 1;
                if (matrix[i][j] >= matrix[i - 1][j]) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j]);
                }
                if (matrix[i][j] >= matrix[i][j - 1]) {
                    dp[i][j] = Math.max(dp[i][j], dp[i][j - 1]);
                }
                max = Math.max(max, dp[i][j]);
            }
        }



        for (int j = 1; j < n; j++) {
            if (matrix[0][j] <= matrix[0][j - 1]) {
                dp[0][j] = dp[0][j - 1] + 1;
            } else {
                dp[0][j] = 1;
            }
            max = Math.max(max, dp[0][j]);
        }

        for (int i = 1; i < m; i++) {
            if (matrix[i][0] <= matrix[i - 1][0]) {
                dp[i][0] = dp[i - 1][0] + 1;
            } else {
                dp[i][0] = 1;
            }
             max = Math.max(max, dp[i][0]);
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = 1;
                if (matrix[i][j] <= matrix[i - 1][j]) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - 1][j]);
                }
                if (matrix[i][j] <= matrix[i][j - 1]) {
                    dp[i][j] = Math.max(dp[i][j], dp[i][j - 1]);
                }
                max = Math.max(max, dp[i][j]);
            }
        }

        return max;

    }
}
```

####记忆化搜索
- DFS + 记忆化保存


```java
public class Solution {

    public int longestIncreasingPath(int[][] matrix) {

        int m = matrix.length;
        if (m == 0) {
            return 0;
        }
        int n = matrix[0].length;
        if (n == 0) {
            return 0;
        }

        int[][] visited = new int[m][n];

        //Java会为数组自动初始化,所以初始化可以不用写
        // for (int i = 0; i < m; i++) {
        //     for (int j = 0; j < n; j++) {
        //         visited[i][j] = 0;
        //     }
        // }

        int max = 1;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                max = Math.max(max, dfs(i, j, m, n, matrix, visited));
            }
        }
        return max;
    }

    public int dfs(int i, int j, int m, int n, int[][] matrix, int[][] visited) {
        if (visited[i][j] != 0) {
            return visited[i][j];
        }

        int[] x = new int[]{0, 1, 0, -1};
        int[] y = new int[]{-1, 0, 1, 0};

        int max = 0;
        for (int k = 0; k < 4; k++) {
            int nx = i + x[k];
            int ny = j + y[k];
            if ( nx >= 0 && nx < m && ny >= 0 && ny < n && matrix[i][j] < matrix[nx][ny]) {
                max = Math.max(dfs(i + x[k], j + y[k], m, n, matrix, visited), max);
            }
        }
        visited[i][j] = max + 1;

        return visited[i][j];

    }
}
```
