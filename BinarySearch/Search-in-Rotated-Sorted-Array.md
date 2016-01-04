##Search in Rotated Sorted Array


	Suppose a sorted array is rotated at some pivot unknown to you beforehand.

	(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

	You are given a target value to search. If found in the array return its index, otherwise return -1.

	You may assume no duplicate exists in the array.

####Tag
- Binary Search
- Array

####思路
- 先找到最小值
- 再通过最小值去判断要找的值在上段还是下段
- 就变成了一般的binary search问题


```java
public class Solution {

    public int[] binarysearch(int start, int end, int nums[], int target) {
        int[] result = new int[2];
        while (start < end - 1) {
            int mid = start + (end -start) / 2;
            if (nums[mid] >= target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
            }
        }
        result[0] = start;
        result[1] = end;
        return result;

    }
    public int search(int[] nums, int target) {
        if (nums.length == 0) {
            return -1;
        }
        int start = 0;
        int end = nums.length - 1;
        int index_max, index_min;
        int[] result = new int[2];

        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (nums[mid] >= nums[end]) {
                start = mid;
            } else if (nums[mid] < nums[end]) {
                end = mid;
            }
        }

        if (nums[start] >= nums[end]) {
            index_max = start;
            index_min = end;
        } else {
            index_max = end;
            index_min = start;
        }

        if (target > nums[nums.length - 1]) {
            start = 0;
            end = index_max;
            result = binarysearch(start, end, nums, target);
            start = result[0];
            end = result[1];
        } else {
            start = index_min;
            end = nums.length - 1;
            result = binarysearch(start, end, nums, target);
            start = result[0];
            end = result[1];
        }

        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
}
```
