##Coins in a Line

	There are n coins in a line. Two players take turns to take one or two coins from right side until there are no more coins left. The player who take the last coin wins.

	Could you please decide the first play will win or lose?

	Have you met this question in a real interview? Yes
	Example
	n = 1, return true.

	n = 2, return true.

	n = 3, return false.

	n = 4, return true.

	n = 5, return true.

####Challenge
O(n) time and O(1) memory

####Tags Expand
Greedy Dynamic Programming Array Game Theory

####思路
- 特殊规律

```java
public class Solution {
    /**
     * @param n: an integer
     * @return: a boolean which equals to true if the first player will win
     */
    public boolean firstWillWin(int n) {
        // write your code here
       return n % 3 != 0;
    }
}

```

####动态规划
- 参考九章算法
- coins类题目

```java
public class Solution {

    public boolean firstWillWin(int n) {
        // write your code here
        if (n <= 0 || n == 3) {
            return false;
        }
        if (n <= 2) {
           return true;
        }


       boolean[] dp = new boolean[n + 1];
       //dp[0] = true;
       dp[1] = true;
       dp[2] = true;
       dp[3] = false;
       dp[4] = true;
       for (int i = 5; i <= n; i++) {
           dp[i] = (dp[i - 3] && dp[i - 4]) || (dp[i - 3] && dp[i - 2]);
       }
       return dp[n];
    }
}

```
