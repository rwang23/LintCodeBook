##3Sum Smaller
	Total Accepted: 8038 Total Submissions: 21165 Difficulty: Medium
	Given an array of n integers nums and a target, find the number of index triplets i, j, k with 0 <= i < j < k < n that satisfy the condition nums[i] + nums[j] + nums[k] < target.

	For example, given nums = [-2, 0, 1, 3], and target = 2.

	Return 2. Because there are two triplets which sums are less than 2:

	[-2, 0, 1]
	[-2, 0, 3]
	Follow up:
	Could you solve it in O(n2) runtime?

####思路
- 3 sum

```java
public class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int n = nums.length;
        Arrays.sort(nums);
        int count = 0;

        for (int i = 0; i < n - 2; i++) {
            int newTarget = target - nums[i];
            int start = i + 1;
            int end = n - 1;
            while (start < end) {
                if (nums[start] + nums[end ] < newTarget) {
                    count += end - start;
                    start++;
                } else {
                    end--;
                }
            }
        }
        return count;
    }
}
```
