##House Robber

30% Accepted

	You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

	Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

	Have you met this question in a real interview? Yes
	Example
	Given [3, 8, 4], return 8.

####Challenge
- O(n) time and O(1) memory.

####Tags Expand
- Dynamic Programming

----

####O(n) time and O(n) memory.
- DP

```java
public class Solution {
    /**
     * @param A: An array of non-negative integers.
     * return: The maximum amount of money you can rob tonight
     */
    public long houseRobber(int[] A) {
        // write your code here
        if (A.length == 0) {
            return 0;
        }
        long[] ret = new long[A.length+1];
        ret[0] = 0;
        ret[1] = A[0];
        long max = ret[1];
        for (int i = 2; i <= A.length; i++) {
            ret[i] = Math.max(ret[i-2]+A[i-1],ret[i-1]);
            max = Math.max(max, ret[i]);
        }
        return max;
    }
}

```
