##Range Sum Query - Immutable
	Total Accepted: 20896 Total Submissions: 85153 Difficulty: Easy
	Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

	Example:
	Given nums = [-2, 0, 3, -5, 2, -1]

	sumRange(0, 2) -> 1
	sumRange(2, 5) -> -1
	sumRange(0, 5) -> -3

####思路
- prefix Sum

```java
public class NumArray {

    int[] prefixSum;
    public NumArray(int[] nums) {

        int size = nums.length;
        prefixSum = new int[size + 1];
        prefixSum[0] = 0;
        for (int i = 1; i <= size; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
        }
    }

    public int sumRange(int i, int j) {
        return prefixSum[j + 1] - prefixSum[i];
    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.sumRange(1, 2);
```
