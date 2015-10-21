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
- 最后求值钱，需要像maximum subarrayII 进行大小值的替换


```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer indicate the value of maximum difference between two
     *          Subarrays
     */
    public int maxDiffSubArrays(ArrayList<Integer> nums) {
        // write your code
        if (nums == null || nums.size() < 2) {
            return 0;
        }
        int[] leftmax = new int[nums.size()];
        int[] rightmax = new int[nums.size()];
        int[] leftmin = new int[nums.size()];
        int[] rightmin = new int[nums.size()];

        leftmax[0] = nums.get(0);
        for (int i = 1; i < nums.size(); i++) {
            leftmax[i] = nums.get(i) + (leftmax[i-1] > 0 ? leftmax[i-1] : 0);
        }
        leftmin[0] = nums.get(0);
        for (int i = 1; i < nums.size(); i++) {
            leftmin[i] = nums.get(i) + (leftmin[i-1] < 0 ? leftmin[i-1] : 0);
        }
        rightmax[nums.size() - 1] = nums.get(nums.size() - 1);
        for (int i = nums.size() - 2; i >= 0; i--) {
            rightmax[i] = nums.get(i) + (rightmax[i+1] > 0 ? rightmax[i+1] : 0);
        }
        rightmin[nums.size() - 1] = nums.get(nums.size() - 1);
        for (int i = nums.size() - 2; i >= 0; i--) {
            rightmin[i] = nums.get(i) + (rightmin[i+1] < 0 ? rightmin[i+1] : 0);
        }

        int max = Math.max(Math.abs(leftmax[0] - rightmin[1]),Math.abs(leftmin[0] - rightmax[1]));
        for (int i = 1; i < nums.size() - 1; i++) {
            if (leftmax[i] < leftmax[i-1]) {
                leftmax[i] = leftmax[i-1];
            }
            if (rightmax[nums.size() - i] > rightmax[nums.size() - 1 - i]) {
                rightmax[nums.size() - i - 1] = rightmax[nums.size() - i];
            }
            if (leftmin[i] > leftmin[i-1]) {
                leftmin[i] = leftmin[i-1];
            }
            if (rightmin[nums.size() - i] < rightmin[nums.size() - 1 - i]) {
                rightmin[nums.size() - i - 1] = rightmin[nums.size() - i];
            }
            max = Math.max(Math.max(Math.abs(leftmax[i] - rightmin[i+1]), Math.abs(leftmin[i] - rightmax[i+1])), max);
        }
        return max;
    }
}



```
