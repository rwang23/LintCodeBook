##Minimum Size Subarray Sum

23% Accepted

	Given an array of n positive integers and a positive integer s,
	find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return -1 instead.

	Have you met this question in a real interview? Yes
	Example
	Given the array [2,3,1,2,4,3] and s = 7,
	the subarray [4,3] has the minimal length under the problem constraint.

	Challenge
	If you have figured out the O(n) solution,
	try coding another solution of which the time complexity is O(n log n).

####Tags Expand
- Two Pointers Array

####暴力解法 O(n2)
```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @param s: an integer
     * @return: an integer representing the minimum size of subarray
     */
    public int minimumSize(int[] nums, int s) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int size = nums.length;
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < size; i++) {
            int sum = 0;
            int length = 0;
            for (int j = i; j < size; j++) {
                sum = sum + nums[j];
                length++;
                if (sum >= s) {
                    min = Math.min(min, length);
                }
            }
        }
        if (min != Integer.MAX_VALUE){
            return min;
        } else {
            return -1;
        }
    }
}

```

####优化解法 O(n)
- 前向型two pointers
- 先想清楚规律,自己画图找i j范围
- 已经[0,4] 已经找到满足条件,就不需要找[0,5] [0,6] 了
- 然后i++ sum 减去nums[i] 变成[1,4]去找是否满足,如果满足,就不用找[1,5],而是i++去找[2,4]
- 如果不满足 就去找[1,5]

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @param s: an integer
     * @return: an integer representing the minimum size of subarray
     */
    public int minimumSize(int[] nums, int s) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int size = nums.length;
        int min = Integer.MAX_VALUE;
        int sum = 0;
        int length = 0;
        for (int i = 0,  j = 0; i < size && j <= size; i++) {
            if (i != 0) {
                sum = sum - nums[i-1];
                length--;
            }

            while (sum < s && j < size) {
                sum = sum + nums[j++];
                length++;
            }

            if (sum >= s) {
                min = Math.min(min, length);
            }

        }

        return min == Integer.MAX_VALUE ? -1 : min;

    }
}

```
