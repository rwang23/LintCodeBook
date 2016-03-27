##Wiggle Sort

	Total Accepted: 9167 Total Submissions: 18537 Difficulty: Medium
	Given an unsorted array nums, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

	For example, given nums = [3, 5, 2, 1, 6, 4], one possible answer is [1, 6, 2, 5, 3, 4].

####思路
- One pass,遍历过程一边赋值
- 方法其实很多,可以先quick sort再把一小一大赋值过来
- 不过因为想到题目并没有要求sort,所以应该是不需要o(nlogn)的方法,由此就想到是不是可以用0(n)做成

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        if (nums == null || nums.length <= 1) {
            return;
        }

        for (int i = 1; i < nums.length; i++) {
            int max = Math.max(nums[i], nums[i - 1]);
            int min = Math.min(nums[i], nums[i - 1]);
            if (i % 2 == 1) {
                nums[i - 1] = min;
                nums[i] = max;
            } else if (i % 2 == 0) {
                nums[i - 1] = max;
                nums[i] = min;
            }
        }
    }
}
```
