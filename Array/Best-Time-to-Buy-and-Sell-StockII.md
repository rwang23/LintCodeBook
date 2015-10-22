##Best Time to Buy and Sell Stock II Show result

50% Accepted

	Say you have an array for which the ith element is the price of a given stock on day i.

	Design an algorithm to find the maximum profit.
    You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times).
    However, you may not engage in multiple transactions at the same time
    (ie, you must sell the stock before you buy again).

	Have you met this question in a real interview? Yes
	Example
	Given an example [2,1,2,0,1], return 2

####Tags Expand
- Greedy
- Enumeration
- Array

####思路
- 后一个price大于前一个，就加上 prices[i] - prices[i-1]

```java
class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int[] prices) {
        // write your code here
        int sum = 0;
        for (int i = 1; i < prices.length; i++) {
            sum = sum + (prices[i] > prices[i-1] ? prices[i] - prices[i-1] : 0);
        }
        return sum;
    }
};

```
