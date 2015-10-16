##Partition Array

25% Accepted

	Given an array nums of integers and an int k, partition the array (i.e move the elements in "nums") such that:

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
- quick select

```java
public class Solution {
	/**
     *@param nums: The integer array you should partition
     *@param k: As description
     *return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
	    //write your code here
	    if (nums == null || nums.length == 0) {
	        return 0;
	    }
	    int lo = 0;
	    int hi = nums.length - 1;
	    while (lo < hi) {
            int j = partition(nums, lo, hi);
            if (nums[j] >= k) {
                hi = j - 1;
            } else if (nums[j] < k) {
                lo = j + 1 ;
            }
	    }
	    int min = k;
	    for (int i = 0; i < nums.length; i++) {
	        if (nums[i] == k) {
	            return i;
	        }
	        min = Math.min(min, nums[i]);
	    }
	    if (min == k) {
	        return 0;
	    } else {
	        return nums.length;
	    }
    }

    public int partition(int[] nums, int lo, int hi) {
        int i = lo;
	    int j = hi+1;
	    while (true) {
	        while (nums[--j] > nums[lo]) {
	            if (j == lo) {
	                break;
	            }
	        }
	        while (nums[++i] < nums[lo]) {
	            if (i == hi) {
	                break;
	            }
	        }
	        if (i >= j) {
	            break;
	        }
	        swap(nums, i, j);
	    }
	    swap(nums, lo, j);
	    return j;
    }
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}

```

####更简洁解法
- 没有局限于quick sort
- 用quick sort的思想，使用两个指针

```java
public class Solution {
	/**
     *@param nums: The integer array you should partition
     *@param k: As description
     *return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
        int i = 0, j = nums.length - 1;
        while (i <= j) {
            while (i <= j && nums[i] < k) i++;
            while (i <= j && nums[j] >= k) j--;
            if (i <= j) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
                i++;
                j--;
            }
        }
        return i;
    }
}

```
