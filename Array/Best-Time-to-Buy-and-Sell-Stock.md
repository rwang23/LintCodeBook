##Best Time to Buy and Sell Stock

41% Accepted

	Say you have an array for which the ith element is the price of a given stock on day i.

	If you were only permitted to complete at most one transaction
    (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

	Have you met this question in a real interview? Yes
	Example
	Given an example [3,2,3,1,2], return 1

####Tags Expand
- Greedy
- Enumeration
- Array

####思路
- 利用了动规的思想，不断找prices[i]前里边的利润最大值
- i不断向后移，找i-1前边最小的数，i-1和i的最大值

```java
public class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int[] prices) {
        // write your code here
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int min = prices[0];
        int max = prices[1];
        int revenue = Math.max(max - min, 0);
        for (int i = 2; i < prices.length; i++) {
            max = Math.max(prices[i-1],prices[i]); //多此一举，直接使用prices[i]就可以
            min = Math.min(min,prices[i-1]);
            revenue = Math.max(revenue, max - min);
        }
        return revenue;
    }
}

```

####稍微优化
```java
public class Solution {
    /**
     * @param prices: Given an integer array
     * @return: Maximum profit
     */
    public int maxProfit(int[] prices) {
        // write your code here
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int min = prices[0];
        //int max = prices[1];
        int revenue = Math.max(prices[1] - min, 0);
        for (int i = 2; i < prices.length; i++) {
            //max = prices[i];
            min = Math.min(min,prices[i-1]);
            revenue = Math.max(revenue, prices[i] - min);
        }
        return revenue;
    }
}

```
