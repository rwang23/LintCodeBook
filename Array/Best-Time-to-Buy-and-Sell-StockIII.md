##Best Time to Buy and Sell Stock III

26% Accepted

	Say you have an array for which the ith element is the price of a given stock on day i.

	Design an algorithm to find the maximum profit. You may complete at most two transactions.

	Have you met this question in a real interview? Yes
	Example
	Given an example [4,4,6,1,1,4,2,5], return 6.

	Note
	You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

####Tags Expand
- Enumeration
- Forward-Backward
- Traversal Array

####思路
- 具体方法跟I差不多，只是思想不同
- 先找从左开始的最大值，存在数组里，再找从右开始的最大值，存在数组里
- 从左开始找的时候，一直使用数组中最小值，然后用最新的i找到值相减得到最大差
- 从右开始找的时候反过来，从length-2（因为length -1是初值）开始，不断找到最大值，再减去最新的i找到的值相减得到最大差
- 最后再合并，找出同一个i时，左右相加最大值
- 利用了分治的思想


```java
public class Solution {
    public int maxProfit(int k, int[] prices) {

        int days = prices.length;

        if (days == 0 || k == 0) {
            return 0;
        }

        if (k > days) {
            return maxProfit(days, prices);
        }

        int[][] transact = new int[days][k];

        for (int i = 0; i < days; i++) {
            transact[i][0] = 0;
        }
        for (int i = 0; i < k; i++) {
            transact[0][i] = 0;
        }

        int globalMax = 0;
        for (int i = 1; i < days; i++) {
            for (int j = 1; j <= i && j < k; j++) {
                int localMax = 0;
                int localMin = prices[j - 1];
                for (int x = j; x <= i; x++) {
                    localMax = Math.max(prices[x] - localMin, localMax);
                    localMin = Math.min(prices[x], localMin);
                    transact[i][j] = Math.max(transact[i - 1][j], transact[x][j - 1] + localMax);
                }
                globalMax = Math.max(globalMax, transact[i][j]);
            }
        }
        return globalMax;
    }

}
```
