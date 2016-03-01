##Best Time to Buy and Sell Stock with Cooldown

	Total Accepted: 9589 Total Submissions: 26741 Difficulty: Medium
	Say you have an array for which the ith element is the price of a given stock on day i.

	Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

	You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
	After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
	Example:

	prices = [1, 2, 3, 0, 2]
	maxProfit = 3
	transactions = [buy, sell, cooldown, buy, sell]

####思路
- 动态规划
- [常规想法](https://leetcode.com/discuss/71354/share-my-thinking-process)
- 这个[参考非常棒,使用了state machine来进行动态规划](https://leetcode.com/discuss/72030/share-my-dp-solution-by-state-machine-thinking)
- 我的解法参考了state machine解法,其实优化过后就是正常解法
- state machine为以后动态规划多个状态提供了一个思路

```java
public class Solution {
    public int maxProfit(int[] prices) {
        int days = prices.length;

        if (days <= 1) {
            return 0;
        }

        /*
        state0代表正在冷却期
        state1代表已经购买了
        state2代表已经卖出了
         */
        int[] state0 = new int[days + 1];
        int[] state1 = new int[days + 1];
        //int[] state2 = new int[days + 1];
        int state2 = 0;

        state0[0] = 0;
        /*
        这个初始化很容易错,
        正在冷却期下一步一定是购买了,
        所以初始化为-prices[0],
        否则动规方程中永远减不下去,一直为0
         */
        state1[0] = -prices[0];

        for (int i = 1; i <= days; i++) {
            state1[i] = Math.max(state1[i - 1], state0[i - 1] - prices[i - 1]);
            //state2[i] = (state1[i - 1] + prices[i - 1]);
            state0[i] = Math.max(state0[i - 1], state2);
            state2 = (state1[i - 1] + prices[i - 1]);
        }

        return Math.max(Math.max(state1[days], state0[days]), state2);

    }
}
```
