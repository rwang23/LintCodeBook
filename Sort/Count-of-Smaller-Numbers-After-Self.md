##Count of Smaller Numbers After Self

	Total Accepted: 6186 Total Submissions: 21480 Difficulty: Hard
	You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

	Example:

	Given nums = [5, 2, 6, 1]

	To the right of 5 there are 2 smaller elements (2 and 1).
	To the right of 2 there is only 1 smaller element (1).
	To the right of 6 there is 1 smaller element (1).
	To the right of 1 there is 0 smaller element.
	Return the array [2, 1, 1, 0].

####思路
- O(n2) 暴力解法

```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        int n = nums.length;
        List<Integer> result = new ArrayList<Integer>();

        if (n == 0) {
            return result;
        }

        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (nums[j] < nums[i]) {
                    result.add(nums[j]);
                }
            }
        }
        return result;
    }
}
```

####优化解法
- 使用逆序数有经典的解法为合并排序
- ?
