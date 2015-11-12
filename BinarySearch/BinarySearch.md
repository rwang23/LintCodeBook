##Binary Search

29% Accepted

    For a given sorted array (ascending order) and a target number,
    find the first index of this number in O(log n) time complexity.

    If the target number does not exist in the array, return -1.

	Example
	If the array is [1, 2, 3, 3, 4, 5, 10], for given target 3, return 2.

####Challenge
- If the count of numbers is bigger than 2^32, can your code work properly?

####Tags Expand
- Binary Search
- Array

####思路
- 使用了end > start + 1是为了避免进入死循环，之后用两个if单独判断弥补，这样避免死循环很有效
- mid = start + (end - start) / 2; 防止了溢出

```java
class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        //write your code here
        if (nums.length == 0 || nums == null) {
            return -1;
        }
        int end = nums.length-1;
        int start = 0;

        while (end > start + 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                end = mid;
            } else if(nums[mid] > target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (nums[end] == target) {
            return end;
        } else if(nums[start] == target) {
            return start;
        }

        return -1;
    }
}

```
