##Maximum Subarray III

23% Accepted

	Given an array of integers and a number k,
    find k non-overlapping subarrays which have the largest sum.

	The number in each subarray should be contiguous.

	Return the largest sum.

	Have you met this question in a real interview? Yes
	Example
	Given [-1,4,-2,3,-2,3], k=2, return 8

	Note
	The subarray should contain at least one number

####Tags Expand
LintCode Copyright Dynamic Programming Subarray Array


####思路
- 动态规划难题
- 思路来源：[雯雯熊孩子](http://blog.csdn.net/nicaishibiantai/article/details/44585383)
- state: aux[i][j]代表0->i-1元素中j个subarray的maxsum  (注意不包含元素i)
- function: aux[i][j] = max(aux[i][j], aux[m][j-1] + max) (m = j-1 .... i-1;  这里的aux[i][j]是在循环里，所以取aux[i][j]的最大值
- function details： max是从元素j-1到i-1（i-1因为aux[i][j]代表0->i-1元素中，j-1因为题目中说“The subarray should contain at least one number”）的max subarray, 用求maximum subarray的方法，需要从后往前算
- initialize: aux[i][j]都为最小值
- answer: aux[len][k]代表了 len-1元素中k段subarray的最大和


```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: An integer denote to find k non-overlapping subarrays
     * @return: An integer denote the sum of max k non-overlapping subarrays
     */
    public int maxSubArray(ArrayList<Integer> nums, int k) {
        // write your code
        int len = nums.size();
        int[][] aux = new int[len+1][k+1];
        for (int j = 1; j <= k; j++) {
            for (int i = j; i <= len; i++) {
                aux[i][j] = Integer.MIN_VALUE;
                int max = Integer.MIN_VALUE;
                int localMax = 0;
                for (int m = i-1; m >= j-1; m--) {
                    localMax = Math.max(nums.get(m), nums.get(m)+localMax);
                    max = Math.max(localMax, max);
                    aux[i][j] = Math.max(aux[i][j], aux[m][j-1] + max);
                }
            }
        }
        return aux[len][k];
    }
}


```
