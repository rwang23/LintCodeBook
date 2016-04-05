##Increasing Triplet Subsequence

	Total Accepted: 9732 Total Submissions: 29385 Difficulty: Medium
	Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

	Formally the function should:
	Return true if there exists i, j, k
	such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.
	Your algorithm should run in O(n) time complexity and O(1) space complexity.

	Examples:
	Given [1, 2, 3, 4, 5],
	return true.

	Given [5, 4, 3, 2, 1],
	return false.

####思路
- 动态规划O(n2)
- 动规可以解决k个数的问题
- 但是三个数可以三个指针直接做O(n)

```java
public class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) {
            return false;
        }

        int size = nums.length;
        int[] increasingNum = new int[size];
        for (int i = 0; i < size; i++) {
            increasingNum[i] = 1;
        }

        for (int i = 1; i < size; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    increasingNum[i] = Math.max(increasingNum[i], increasingNum[j] + 1);
                }
                if (increasingNum[i] == 3) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

####三个指针
- 第一个指针存最小值,第二个指针存大于最小值的值,第三个指针存最大值(写的过程中优化后省略了)
- 判断的时候是<=,否则如果等于的话就进入下一层条件,就错误了

```java
public class Solution {
    public boolean increasingTriplet(int[] nums) {
        if (nums == null || nums.length < 3) {
            return false;
        }

        int size = nums.length;
        int firstMin = Integer.MAX_VALUE;
        int secondMin = Integer.MAX_VALUE;
        //int max = Integer.MIN_VALUE;

        for (int i = 0; i < size; i++) {
            if (nums[i] <= firstMin) {
                firstMin = nums[i];
            } else if (nums[i] <= secondMin) {
                secondMin = nums[i];
            } else {
                //max = nums[i];
                return true;
            }
        }

        return false;
    }
}
```
