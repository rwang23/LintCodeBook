##Recover Rotated Sorted Array

26% Accepted

	Given a rotated sorted array, recover it to sorted array in-place.

	Have you met this question in a real interview? Yes
	Example
	[4, 5, 1, 2, 3] -> [1, 2, 3, 4, 5]

####Challenge
- In-place, O(1) extra space and O(n) time.

####Clarification

	What is rotated array?

	For example, the orginal array is [1,2,3,4], The rotated array of it can be [1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]

####Tags Expand
Sorted Array

####思路
- 左边翻转，右边翻转，整体翻转

```java
public class Solution {
    /**
     * @param nums: The rotated sorted array
     * @return: The recovered sorted array
     */
    private void reverse(ArrayList<Integer> nums, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            int temp = nums.get(i);
            nums.set(i, nums.get(j));
            nums.set(j, temp);
        }
    }

    public void recoverRotatedSortedArray(ArrayList<Integer> nums) {
        for (int index = 0; index < nums.size() - 1; index++) {
            if (nums.get(index) > nums.get(index + 1)) {
                reverse(nums, 0, index);
                reverse(nums, index + 1, nums.size() - 1);
                reverse(nums, 0, nums.size() - 1);
                return;
            }
        }
    }
}
```
