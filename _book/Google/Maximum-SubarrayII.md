##Maximum Subarray II

24% Accepted

    Given an array of integers, find two non-overlapping subarrays which have the largest sum.

    The number in each subarray should be contiguous.

    Return the largest sum.

    Have you met this question in a real interview? Yes
    Example
    For given [1, 3, -1, 2, -1, 2], the two subarrays are [1, 3] and [2, -1, 2] or [1, 3, -1, 2] and [2], they both have the largest sum 7.

    Note
    The subarray should contain at least one number

    Challenge
    Can you do it in time complexity O(n) ?

####Tags Expand
- Greedy
- Enumeration
- Array
- LintCode Copyright
- Subarray
- Forward-Backward Traversal

####思路
- 具体方法跟I差不多，只是思想不同
- 先找从左开始的最大值，存在数组里，再找从右开始的最大值，存在数组里
- 最后再合并，找出同一个i时，左右相加最大值
- 之后记得left right重新赋值，最开始的left right是算的当时最大值，需要赋值为i前最大值
- 利用了分治的思想


```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: An integer denotes the sum of max two non-overlapping subarrays
     */
    public int maxTwoSubArrays(ArrayList<Integer> nums) {
        // write your code
        if (nums == null || nums.size() < 2) {
            return 0;
        }
        int[] left = new int[nums.size()];
        int[] right = new int[nums.size()];

        left[0] = nums.get(0);
        for (int i = 1; i < nums.size(); i++) {
            left[i] = nums.get(i) + (left[i-1] > 0 ? left[i-1] : 0);
        }

        right[nums.size() - 1] = nums.get(nums.size() - 1);
        for (int i = nums.size() - 2; i >= 0; i--) {
            right[i] = nums.get(i) + (right[i+1] > 0 ? right[i+1] : 0);
        }

        int max = left[0] + right[1];
        for (int i = 1; i < nums.size() - 1; i++) {
            if (left[i] < left[i-1]) {
                left[i] = left[i-1];
            }
            if (right[nums.size() - i] > right[nums.size() - 1 - i]) {
                right[nums.size() - i - 1] = right[nums.size() - i];
            }
            //max = Math.max(max, left[i] + right[i+1]);
        }

        for (int i = 1; i < nums.size() - 1; i++) {
            max = Math.max(max, left[i] + right[i+1]);
        }

        return max;
    }
}





```
