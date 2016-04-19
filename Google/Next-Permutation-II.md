##Next Permutation II

32% Accepted

		Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

		If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

		Have you met this question in a real interview? Yes
		Example
		Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

		1,2,3 → 1,3,2

		3,2,1 → 1,2,3

		1,1,5 → 1,5,1

####Challenge
The replacement must be in-place, do not allocate extra memory.

####Tags Expand
- Permutation Array

####思路

	permutation iterative固定做法
	从后往前寻找索引满足 a[k] < a[k + 1], 如果此条件不满足，则说明已遍历到最后一个。
	从后往前遍历，找到第一个比a[k]大的数a[l], 即a[k] < a[l].
	交换a[k]与a[l].
	反转k + 1 ~ n之间的元素。
	input [1,3,2]
	第一步,发现1 < 3 所以 i 指向的是1这个元素 = 0
	第二步,从后面往前找第一个比1大的数,发现是2,index是2
	第三步,交换a[0] a[2] 数组变成[2,3,1]
	第四步, 翻转i+1 到最后 数组变成[2,1,3]
	得到答案


```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: return nothing (void), do not return anything, modify nums in-place instead
     */
    //Reverse the given part of a int[]
    public int[] reverse(int start, int end, int[] nums) {
    	for (int i = start, j = end; i < j; i++,j--) {
    		int temp = nums[i];
    		nums[i] = nums[j];
    		nums[j] = temp;
    	}
    	return nums;
    }

    public int[] nextPermutation(int[] nums) {
    	if (nums == null || nums.length == 0) {
    		return nums;
    	}
    	//Find last increasing point before decreasing. nums[k] < nums[k+1]
    	int k = -1;
    	for (int i = nums.length - 2; i >= 0; i--) {
    		if (nums[i] < nums[i + 1]) {
    			k = i;
    			break;
    		}
    	}
    	if (k == -1) {
    		return reverse(0, nums.length - 1, nums);
    	}
    	//Find first bigger point, from right to left
    	int bigIndex = -1;
    	for (int i = nums.length - 1; i >= 0; i--) {
    		if (nums[i] > nums[k]) {
    			bigIndex = i;
    			break;
    		}
    	}
    	//1. Swap bigger index with k;
    	//2. Reverse the right side of k.
    	//[Try to make the smallest next permutation]
    	int temp = nums[k];
    	nums[k] = nums[bigIndex];
    	nums[bigIndex] = temp;

    	return reverse(k + 1, nums.length - 1, nums);
    }

}


```
