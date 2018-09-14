##Partition Array

25% Accepted

	Given an array nums of integers and an int k, partition the array
	(i.e move the elements in "nums") such that:

	All elements < k are moved to the left
	All elements >= k are moved to the right
	Return the partitioning index, i.e the first index i nums[i] >= k.

	Have you met this question in a real interview? Yes
	Example
	If nums = [3,2,2,1] and k=2, a valid answer is 1.

	Note
	You should do really partition in array nums instead of just counting the numbers of integers smaller than k.

	If all elements in nums are smaller than k, then return nums.length

####Challenge
Can you partition the array in-place and in O(n)?

####Tags Expand
Two Pointers Sort Array

####思路
- 用quick sort的思想，使用两个指针

```java
public class Solution {
    /**
     * @param nums: The integer array you should partition
     * @param k: An integer
     * @return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            while (left <= right && nums[left] < k) {
                left++;
            }

            while (left <= right && nums[right] >= k) {
                right--;
            }

            if (left <= right) {
                swap(nums, left++, right--);
            }
        }

        return left;
    }

    public void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}

```
