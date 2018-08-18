##Maximum Number in Mountain Sequence
[lintcode](https://www.lintcode.com/problem/maximum-number-in-mountain-sequence/description?_from=ladder)

	Given a mountain sequence of n integers which increase firstly and then decrease, find the mountain top.

##Example
	Given nums = [1, 2, 4, 8, 6, 3] return 8
	Given nums = [10, 9, 8, 7], return 10

##思路
```java
public class Solution {
    /**
     * @param nums: a mountain sequence which increase firstly and then decrease
     * @return: then mountain top
     */
    public int mountainSequence(int[] nums) {
        // write your code here
        if (nums.length == 1) {
            return nums[0];
        }

        if (nums.length > 1 && nums[0] > nums[1]) {
            return nums[0];
        }

        int start = 0;
        int end = nums.length - 1;
        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1]) {
                return nums[mid];
            } else if (nums[mid] > nums[mid - 1]) {
                start = mid;
            } else if (nums[mid] < nums[mid - 1]) {
                end = mid;
            }
        }
        return 0;
    }
}
```
