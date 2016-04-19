##Search in Rotated Sorted Array II

	Total Accepted: 60092 Total Submissions: 188639 Difficulty: Medium
	Follow up for "Search in Rotated Sorted Array":
	What if duplicates are allowed?

	Would this affect the run-time complexity? How and why?

	Write a function to determine if a given target is in the array.

####思路
- 我的思路是先找到最低点的index,找的时候有两种情况,一种要从end--开始找,一种是start++开始找
- 然后通过index划分两边,再对两边分别进行binary search,找是否有target
- 平均O(logn),最坏情况O(n)
- 也可以直接做,[参考](https://leetcode.com/discuss/30308/java-solution-with-comments)

```java
public class Solution {
    public boolean search(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return false;
        }
        int len = nums.length;
        int lowIndex1 = searchLowestIndex1(nums);
        int lowIndex2 = searchLowestIndex2(nums);
        return binarySearch(nums, target, 0, lowIndex1 - 1) || binarySearch(nums, target, lowIndex1, len - 1) || binarySearch(nums, target, 0, lowIndex2 - 1) || binarySearch(nums, target, lowIndex2, len - 1);
    }

    public int searchLowestIndex1(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int len = nums.length;
        int start = 0;
        int end = len - 1;

        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == nums[end]) {
                end--;
            } else if (nums[mid] > nums[end]) {
                start = mid;
            } else {
                end = mid;
            }
        }

        return (nums[start] < nums[end]) ? start : end;
    }

    public int searchLowestIndex2(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int len = nums.length;
        int start = 0;
        int end = len - 1;

        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == nums[start]) {
                start++;
            } else if (nums[mid] > nums[start]) {
                start = mid;
            } else {
                end = mid;
            }
        }

        return (nums[start] < nums[end]) ? start : end;
    }

    public boolean binarySearch(int[] nums, int target, int start, int end) {
        if (end < start || start < 0) {
            return false;
        }

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return true;
            } else if (nums[mid] > target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        return (nums[start] == target) || (nums[end] == target);
    }
}
```
