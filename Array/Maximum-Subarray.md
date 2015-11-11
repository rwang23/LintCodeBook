##Maximum Subarray Show result

37% Accepted

	Given an array of integers, find a contiguous subarray which has the largest sum.

	Have you met this question in a real interview? Yes
	Example
	Given the array [−2,2,−3,4,−1,2,1,−5,3], the contiguous subarray [4,−1,2,1] has the largest sum = 6.

	Note
	The subarray should contain at least one number.

####Challenge
Can you do it in time complexity O(n)?

####Tags Expand
- Greedy
- Enumeration
- LintCode Copyright
- Subarray Array

####思路
- 动态规划
- 从第一个数就要开始思考
- state: sum[i]是前i个数中，最大的subarray sum
- function: sum[i] = A[i] + (sum[i-1] > 0 ? sum[i-1] ：0) 因为是连续的，所以要加上A[i]，如果前面和大于零，就加上
- initialize: sum[0] = A[0]
- answer: 设置一个max去存最大值
- 优化： 因为就用到了sum[i]和sum[i-1],所以用两个寄存器就可以了，没必要用数组

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A integer indicate the sum of max subarray
     */
     public int maxSubArray(int[] A) {
        // write your code
        if (A == null || A.length == 0) {
            return Integer.MIN_VALUE;
        }
        //int[] sum = new int[A.length];
        //sum[0] = A[0];
        int max = A[0];
        int cur;
        int pre = A[0];
        for (int i = 1; i < A.length; i++) {
            cur = A[i] + (pre > 0 ? pre : 0 );
            max = Math.max(max, cur);
            pre = cur;
        }
        return max;
    }
}

```
