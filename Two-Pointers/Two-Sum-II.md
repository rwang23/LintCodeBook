##Two Sum II

23% Accepted

	Given an array of integers, find how many pairs in the array such that their sum is bigger than a specific target number. Please return the number of pairs.

	Example
	numbers=[2, 7, 11, 15], target=24

	return 1

####Challenge
Either of the following solutions are acceptable:
O(1) Space, O(nlogn) Time
####Tags Expand
- Two Pointers

####思路
- 类似于two sum, 但是画图
- 因为是大于不再是等于了,所以不能再使用hashmap来优化了
- 这个时候采取two sum的另一种做法, 利用排序来做
- 这个题还有一些小trick
- 找到 nums[start] + nums[end] > target 并不是count++, 很容易在这里犯错
- 比如[3,4,5,7,8] target = 9
- start = 0 ,end = 4, 3 + 8 > 9, end--
- 这个时候不是count++,因为4+8 5+8 7+8 都会大于target
- 所以是count = count + end - start

```java
public class Solution {
    /**
     * @param nums: an array of integer
     * @param target: an integer
     * @return: an integer
     */
    public int twoSum2(int[] nums, int target) {
        // Write your code here
        Arrays.sort(nums);

        int start = 0;
        int end = nums.length - 1;
        int count = 0;
        while (start < end) {
            if (nums[start] + nums[end] > target) {
                count = count + end - start;
                end--;
            } else if (nums[start] + nums[end] < target) {
                start++;
            } else {
                start++;
            }
        }
        return count;
    }
}

```
