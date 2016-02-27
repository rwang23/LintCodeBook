##Coin Change

	You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

	Example 1:
	coins = [1, 2, 5], amount = 11
	return 3 (11 = 5 + 5 + 1)

	Example 2:
	coins = [2], amount = 3
	return -1.

##Note:
You may assume that you have an infinite number of each kind of coin.

####思路
- 这道题自己Mock Interview遇到了,跪了
- 最开始自己用的DFS,明显超时
- 于是更改方法,DFS+贪心
- 但是贪心会有问题,找出来的不一定是最优解
- 最后在25min内没有解出
- 但是其实用动态规划,就很简单
- 题目很明显了,找最小,想到了动规方案只需要三分钟
- dp，设dp[i] 为兑换目标i最少的硬币数。
- 则有：dp[i + coins[j] ] = min(dp[i + coins[j] ] , dp[i] + 1）

```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins.length == 0 && amount == 0) {
            return 0;
        }
        if (amount < 0) {
            return -1;
        }

        int[] dp = new int[amount + 1];
        dp[0] = 0;
        for (int i = 1; i <= amount; i++) {
            dp[i] = Integer.MAX_VALUE;
        }


        for (int j = 0; j < coins.length; j++) {
            for (int i = 0; i + coins[j]  <= amount; i++) {
                if (dp[i] != Integer.MAX_VALUE) {
                    dp[i + coins[j]] = Math.min(dp[i + coins[j]], dp[i] + 1);
                }
            }
        }

        return dp[amount] == Integer.MAX_VALUE ? -1 : dp[amount];
    }
}
```
