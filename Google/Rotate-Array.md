##Rotate Array

	Total Accepted: 64166 Total Submissions: 311000 Difficulty: Easy
	Rotate an array of n elements to the right by k steps.

	For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

	Note:
	Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

####思路
- 多次翻转
- 注意问清面试官题意,自己在这个题意理解上错了好几次,这个rotate的意思就相当于在执行>>操作

```java
public class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        if (k == 0) {
            return;
        }
        if (k >= n) {
            k = k % n;
        }

        k = n - k;

        reverse(nums, 0, k - 1);
        reverse(nums, k , n - 1);
        reverse(nums, 0, n - 1);
    }

    public void reverse(int[] nums, int start, int end) {
        if (start >= end) return;

        for (int i = start, j = end; i < j; i++, j--) {
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
    }
}
```
