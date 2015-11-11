##Minimum Subarray

37% Accepted

    Given an array of integers, find the subarray with smallest sum.

    Return the sum of the subarray.

    Have you met this question in a real interview? Yes
    Example
    For [1, -1, -2, 1], return -3

    Note
    The subarray should contain at least one integer.

####Tags Expand
- Greedy
- LintCode Copyright
- Subarray Array

####思路
- 动态规划
- state: sum[i]是前i个数中，最小的subarray sum
- function: sum[i] = A[i] + (sum[i-1] < 0 ? sum[i-1] ：0) 因为是连续的，所以要加上A[i]，如果前面和大于零，就加上
- initialize: sum[0] = A[0]
- answer: 设置一个min去存最小值
- 优化： 因为就用到了sum[i]和sum[i-1],所以用两个寄存器就可以了，没必要用数组

```java
public class Solution {
    /**
     * @param nums: a list of integers
     * @return: A integer indicate the sum of minimum subarray
     */
    public int minSubArray(ArrayList<Integer> A) {
        // write your code
        if (A == null || A.size() == 0) {
            return Integer.MIN_VALUE;
        }
        //int[] sum = new int[A.length];
        //sum[0] = A[0];
        int min = A.get(0);
        int cur;
        int pre = A.get(0);
        for (int i = 1; i < A.size(); i++) {
            cur = A.get(i) + (pre < 0 ? pre : 0 );
            min = Math.min(min, cur);
            pre = cur;
        }
        return min;
    }
}



```
