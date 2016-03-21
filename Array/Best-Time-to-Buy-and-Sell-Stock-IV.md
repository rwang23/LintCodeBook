##Best Time to Buy and Sell Stock IV

	Total Accepted: 22656 Total Submissions: 105085 Difficulty: Hard
	Say you have an array for which the ith element is the price of a given stock on day i.

	Design an algorithm to find the maximum profit. You may complete at most k transactions.

	Note:
	You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

####思路
- 未优化版本
- state:dp[i][j]代表前i天j次交易带来的最大利润
- 初始化 dp[i][0] = 0 dp[0][j] = 0
- dp[i][j] = Math.max(dp[i-1][j], dp[k][j-1] + (k+1 到i天的交易利润最大))
- 答案dp[m][n]
- 注意当k非常大的时候,大于了两倍Price长度,那么久变成了可以交易任意次,回到了题II

```java
public class Solution {
    public int maxProfit(int k, int[] prices) {

        int days = prices.length;

        if (days == 0 || k == 0) {
            return 0;
        }

        if (k == 1) {
            return maxProfit1(prices);
        }


        if (k >= prices.length / 2) {
            int profit = 0;
            for (int i = 1; i < prices.length; i++) {
                if (prices[i] > prices[i - 1]) {
                    profit += prices[i] - prices[i - 1];
                }
            }
            return profit;
        }

        int[][] transact = new int[days + 1][k + 1];

        for (int i = 0; i <= days; i++) {
            transact[i][0] = 0;
        }
        for (int i = 0; i <= k; i++) {
            transact[0][i] = 0;
        }

        for (int i = 2; i <= days; i++) {
            for (int j = 1; j <= i && j <= k; j++) {
                int maxValue = prices[i - 1];
                int localMax = 0;
                int globalMax = 0;
                for (int x = i - 1; x >= j; x--) {
                    localMax = Math.max(localMax, maxValue - prices[x - 1]);
                    maxValue = Math.max(maxValue, prices[x - 1]);
                    globalMax = Math.max(globalMax, localMax + transact[x][j - 1]);

                }
                transact[i][j] = Math.max(transact[i - 1][j], globalMax);
            }
        }
        return transact[days][k];
    }

        public int maxProfit1(int[] prices) {
        // write your code here
            if (prices == null || prices.length <= 1) {
                return 0;
            }

            int min = prices[0];
            int max = 0;
            for (int i = 1; i < prices.length; i++) {
                int profit = prices[i] - min;
                max = Math.max(max, profit);
                min = Math.min(min, prices[i]);
            }

            return max;
        }

}
```

####优化思路

