##Last Position of Target
[lintcode](https://www.lintcode.com/problem/last-position-of-target/description)

	Find the last position of a target number in a sorted array. Return -1 if target does not exist.

	Example
	Given [1, 2, 2, 4, 5, 5].

	For target = 2, return 2.

	For target = 5, return 5.

	For target = 6, return -1.

##思路

```java
public class Solution {
    /**
     * @param nums: An integer array sorted in ascending order
     * @param target: An integer
     * @return: An integer
     */
    public int lastPosition(int[] nums, int target) {
        // write your code here
        if (nums.length == 0) {
            return -1;
        }

        int start = 0;
        int end = nums.length - 1;
        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > target) {
                end = mid;
            } else if (nums[mid] <= target) {
                start = mid;
            }
        }

        if (nums[end] == target) {
            return end;
        }
        if (nums[start] == target) {
            return start;
        }

        return -1;
    }
}
```
