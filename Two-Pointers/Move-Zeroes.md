##Move Zeroes
	Total Accepted: 78338 Total Submissions: 177188 Difficulty: Easy
	Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

	For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

	Note:
	You must do this in-place without making a copy of the array.
	Minimize the total number of operations.

####思路
- Two pointers

```java
public class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int size = nums.length;
        int i = 0;
        int j = 0;
        while (i < size && j < size) {
            while (i < size && nums[i] != 0) {
                i++;
            }
            j = i + 1;
            while (j < size && nums[j] == 0) {
                j++;
            }

            if (i >= size || j >= size) {
                break;
            }

            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;

        }
    }
}
```
