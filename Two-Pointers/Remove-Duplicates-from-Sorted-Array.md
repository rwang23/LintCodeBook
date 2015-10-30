##Remove Duplicates from Sorted Array

32% Accepted

	Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

	Do not allocate extra space for another array, you must do this in place with constant memory.

	Have you met this question in a real interview? Yes
	Example
	Given input array A = [1,1,2],

Your function should return length = 2, and A is now [1,2].

####Tags Expand
- Two Pointers Array

####思路
- 其实挺难的，需要画图通过两根指针来找规律来写

```java
public class Solution {
    /**
     * @param A: a array of integers
     * @return : return an integer
     */
    public int removeDuplicates(int[] nums) {
        // write your code here
        if (nums == null || nums.length <= 1) {
            return nums.length;
        }

        int i = 0;
        int j = 1;
        while (i < nums.length && j < nums.length) {
        	/*
        	如果出现相同，则j继续向前边找，找到不同于A[i]的那个数
        	 */
            if (nums[i] == nums[j]){
                j++;
            } else {
            	/*
            	i++就是指向之前那个重复的元素，然后好用nums[j] 去替代nums[i]
            	 */
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;

    }
}

```
