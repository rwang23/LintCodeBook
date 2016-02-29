##Coins in a Line III

	There are n coins in a line. Two players take turns to take a coin from one of the ends of the line until there are no more coins left. The player with the larger amount of money wins.

	Could you please decide the first player will win or lose?

	Have you met this question in a real interview? Yes
	Example
	Given array A = [3,2,2], return true.

	Given array A = [1,2,4], return true.

	Given array A = [1,20,4], return false.

####Challenge
Follow Up Question:

	If n is even. Is there any hacky algorithm that can decide whether first player will win or lose in O(1) memory and O(n) time?

####Tags Expand
Dynamic Programming Array Game Theory

####思路
- 画图找规律
- 再通过简单的case代入,去寻找初始化
- 通过初始化写循环条件
- dp[i][j] 此时,先手的人从剩下的硬币 values[i] 到values[j]中,所能获得的最大价值


```java
public class Solution {
    /**
     * @param values: an array of integers
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int[] values) {
        // write your code here
        if (values == null || values.length == 0) {
            return false;
        }
        if (values.length == 1) {
            return true;
        }

        int n = values.length;
        int sum = 0;

        for (int i = 0; i < n; i++) {
            sum += values[i];
        }

        int[][] dp = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = values[i];
        }
        for (int i = 0; i < n - 1; i++) {
            dp[i][i + 1] = Math.max(values[i], values[i + 1]);
        }

        for (int dis = 2; dis < n; dis++ ) {
            for (int i = 0, j = i + dis; i < n - 2 && j < n; i++, j++) {
                int min1 = Math.min(dp[i + 2][j], dp[i + 1][j - 1]) + values[i];
                int min2 = Math.min(dp[i + 1][j - 1], dp[i][j - 2]) + values[j];
                dp[i][j] = Math.max(min1, min2);
            }
        }

        return dp[0][n - 1] > sum / 2 ? true : false;
    }
}
```
