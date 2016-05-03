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


Math idea from https://leetcode.com/discuss/98276/why-factor-2-or-3-the-math-behind-this-problem

If an optimal product contains a factor f >= 4,
then you can replace it with factors 2 and f-2 without losing optimality, as 2*(f-2) = 2f-4 >= f. So you never need a factor greater than or equal to 4,
meaning you only need factors 1, 2 and 3
(and 1 is of course wasteful and you'd only use it for n=2 and n=3, where it's needed).
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

####利用数学规律
```
f(n) = 2 * f(n - 2)
f(n) = 3 * f(n - 3)
f(n) = 4 * f(n - 4) = 2 * f(n - 2)
f(n) = 5 * f(n - 5) = 2 * f(n - 5) + 3 * f(n - 5) = f(n - 3) + f(n - 2) < f(n)
所以得出4以上的就不需要再试了,只需要试到底是乘以2大还是乘以3大
并且可以优化空间复杂度
```

```java

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

        for (int i = 4; i <= n; i++) {
            dp[i] = Math.max(dp[i - 2] * 2, dp[i - 3] * 3);
        }
        return dp[n];
    }
}
```
