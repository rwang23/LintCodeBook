Maximum Subarray Difference

23% Accepted

	Given an array with integers.

	Find two non-overlapping subarrays A and B, which |SUM(A) - SUM(B)| is the largest.

	Return the largest difference.

	Have you met this question in a real interview? Yes
	Example
	For [1, 2, -3, 1], return 6

	Note
	The subarray should contain at least one number

####Challenge
O(n) time and O(n) space.

####Tags Expand
- Greedy
- Enumeration
- Array
- LintCode Copyright
- Subarray
- Forward-Backward Traversal

####思路
- abs(左边的max - 右边的min) 或者abs(左边的min - 右边的max)
- 求max 与 min 在maximum subarray 与 minimum subarray已经做了
- 最后求值前，需要像maximum subarrayII 进行大小值的替换
- 因为需要的是index i 前的最大值,所以要不断替换
- 如果用prefix sum的话,要稍微简单一点


```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two
     *          Subarrays
     */
    public int maxDiffSubArrays(int[] nums) {
        // write your code
        if (nums == null || nums.length < 2) {
            return 0;
        }
        int[] leftmax = new int[nums.length];
        int[] rightmax = new int[nums.length];
        int[] leftmin = new int[nums.length];
        int[] rightmin = new int[nums.length];

        leftmax[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            leftmax[i] = nums[i] + (leftmax[i-1] > 0 ? leftmax[i-1] : 0);
        }
        leftmin[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            leftmin[i] = nums[i] + (leftmin[i-1] < 0 ? leftmin[i-1] : 0);
        }
        rightmax[nums.length - 1] = nums[nums.length - 1];
        for (int i = nums.length - 2; i >= 0; i--) {
            rightmax[i] = nums[i] + (rightmax[i+1] > 0 ? rightmax[i+1] : 0);
        }
        rightmin[nums.length - 1] = nums[nums.length - 1];
        for (int i = nums.length - 2; i >= 0; i--) {
            rightmin[i] = nums[i] + (rightmin[i+1] < 0 ? rightmin[i+1] : 0);
        }

        int max = Math.max(Math.abs(leftmax[0] - rightmin[1]),Math.abs(leftmin[0] - rightmax[1]));
        for (int i = 1; i < nums.length - 1; i++) {
            if (leftmax[i] < leftmax[i-1]) {
                leftmax[i] = leftmax[i-1];
            }
            if (rightmax[nums.length - i] > rightmax[nums.length - 1 - i]) {
                rightmax[nums.length - i - 1] = rightmax[nums.length - i];
            }
            if (leftmin[i] > leftmin[i-1]) {
                leftmin[i] = leftmin[i-1];
            }
            if (rightmin[nums.length - i] < rightmin[nums.length - 1 - i]) {
                rightmin[nums.length - i - 1] = rightmin[nums.length - i];
            }
            //max = Math.max(Math.max(Math.abs(leftmax[i] - rightmin[i+1]), Math.abs(leftmin[i] - rightmax[i+1])), max);
        }

        for (int i = 1; i < nums.length - 1; i++) {
            max = Math.max(Math.max(Math.abs(leftmax[i] - rightmin[i+1]), Math.abs(leftmin[i] - rightmax[i+1])), max);
        }
        return max;
    }
}





```
