##Find Minimum in Rotated Sorted Array

33% Accepted

	Suppose a sorted array is rotated at some pivot unknown to you beforehand.

	(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

	Find the minimum element.

	Have you met this question in a real interview? Yes
	Example
	Given [4, 5, 6, 7, 0, 1, 2] return 0

####Note
    You may assume no duplicate exists in the array.

####Tags Expand
- Binary Search

####思路
- 通过判断与end的关系就可以，然而自己判断num[mid]与num[mid-1]，这样也导致了需要考虑mid-1的边界条件
- 或者判断与start的关系，但是判断start如果是没有rotate的array而是一个纯sorted array就需要考虑另一种情况

####判断与end关系
```java
public class Solution {
    public int findMin(int[] num) {
        int start = 0, end = num.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (num[mid] >= num[end]) { //这个=号不要也可以，因为不会有这种情况
                start = mid;
            } else {
                end = mid;
            }
        }
        if (num[start] < num[end]) {
            return num[start];
        } else {
            return num[end];
        }
    }
}
```
####判断与start关系
```java
public class Solution {
    /**
     * @param nums: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] nums) {
        // write your code here
        if (nums.length == 0) {
            return Integer.MIN_VALUE;
        }
        
        if (nums[0] < nums[nums.length - 1]) {
            return nums[0];
        }
        int start = 0;
        int end = nums.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] >= nums[0]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        return (nums[start] > nums[end]) ? nums[end] : nums[start];
    }
}
```
