##Coins in a Line II

	There are n coins with different value in a line. Two players take turns to take one or two coins from left side until there are no more coins left. The player who take the coins with the most value wins.

	Could you please decide the first player will win or lose?

	Have you met this question in a real interview? Yes
	Example
	Given values array A = [1,2,2], return true.

	Given A = [1,2,4], return false.

####Tags
Dynamic Programming Array Game Theory

####思路
- coins类题目
- 需要注意初始化
- 以及要从test case画出来分析

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
        if (values.length <= 2) {
            return true;
        }

        int n = values.length;
        int[] dp = new int[n + 1];
        dp[1] = values[0];
        dp[2] = values[0] + values[1];
        if (n >= 3) {
            dp[3] = values[0] + values[1];
        }
        if (n >= 4) {
            dp[4] = Math.max(values[0] + values[3], values[0] + values[1]);
        }

        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += values[i];
        }

        for (int i = 5; i <= n; i++) {
            dp[i] = Math.max(Math.min(dp[i - 2], dp[i - 3]) + values[n - i], Math.min(dp[i - 3], dp[i - 4]) + values[n - i] + values[n - i + 1]);
        }

        return dp[n] > sum / 2 ? true : false;
    }
}

```
