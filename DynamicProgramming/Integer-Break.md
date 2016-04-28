##Integer Break

	Total Accepted: 5789 Total Submissions: 14408 Difficulty: Medium
	Given a positive integer n, break it into the sum of at least two positive integers and maximize the product of those integers. Return the maximum product you can get.

	For example, given n = 2, return 1 (2 = 1 + 1); given n = 10, return 36 (10 = 3 + 3 + 4).

	Note: you may assume that n is not less than 2.

	Hint:

	There is a simple O(n) solution to this problem.
	You may check the breaking results of n ranging from 7 to 10 to discover the regularities.

####思路
- 动规
- 但是在i = 1, i = 2, i = 3的情况下不管用,因为存在1的情况

```java
/*
state: dp[i] the maximal product of integer i
function: dp[i] = Math.max(dp[i], dp[j] * (i - j))
initialize : dp[1] = 1
answer: dp[n]
*/

public class Solution {
    public int integerBreak(int n) {
        if (n <= 1) {
            return - 1;
        }

        if (n == 2) {
            return 1;
        }

        if (n == 3) {
            return 2;
        }

        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j < i; j++) {
                dp[i] = Math.max(dp[i], dp[j] * (i - j));
            }
        }
        return dp[n];
    }
}
```
