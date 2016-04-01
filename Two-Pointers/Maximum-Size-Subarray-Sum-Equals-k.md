##Maximum Size Subarray Sum Equals k

	Total Accepted: 4421 Total Submissions: 11312 Difficulty: Easy
	Given an array nums and a target value k, find the maximum length of a subarray that sums to k. If there isn't one, return 0 instead.

	Example 1:
	Given nums = [1, -1, 5, -2, 3], k = 3,
	return 4. (because the subarray [1, -1, 5, -2] sums to 3 and is the longest)

	Example 2:
	Given nums = [-2, -1, 2, 1], k = 1,
	return 2. (because the subarray [-1, 2] sums to 1 and is the longest)

	Follow Up:
	Can you do it in O(n) time?

####思路
- 这道题跟minimum size subarray sum是两道完全不同的题
- 首先这道题是求maximum 而且array中包含负数
- 拿到这种题第一反应就应该是two pointers 和 prefixSum
- 然而这道题two pointer不能做,所以用prefixsum
- 可以不用prefixsum数组,直接用nums
- hashmap处理的时候 逻辑要清晰

```java
public class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int size = nums.length;
        if (size == 0) {
            return 0;
        }

        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        int[] prefixSum = new int[size + 1];
        prefixSum[0] = 0;
        map.put(0, 0);
        int max = 0;
        for (int i = 1; i <= size; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
            if (map.containsKey(prefixSum[i] - k)) {
                max = Math.max(i - map.get(prefixSum[i] - k), max);
            }
            if (!map.containsKey(prefixSum[i])) {
                map.put(prefixSum[i], i);
            }
        }
        return max;
    }
}
```
