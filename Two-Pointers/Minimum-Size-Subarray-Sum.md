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

####O(nlogn)解法
O(nlgn)的解法，这个解法要用到二分查找法，
思路是，我们建立一个比原数组长一位的sums数组，其中sums[i]表示nums数组中[0, i - 1]的和，
然后我们对于sums中每一个值sums[i]，用二分查找法找到子数组的右边界位置，使该子数组之和大于sums[i] + s，然后我们更新最短长度的距离即可。代码如下：

####优化解法 O(n)
- 前提条件是 没有负数
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

        for (int i = 0; i < size; i++) {
            if (nums[i] >= s) {
                return 1;
            }
        }

        int sum = 0;
        int i = 0;
        int j = 0;
        int count = 0;
        int min = Integer.MAX_VALUE;

        for (i = 0; i < size; i++) {

            while (sum < s && j < size) {
                sum += nums[j++];
                count++;
            }
            if (sum >= s) {
                min = Math.min(min, count);
            }
            sum -= nums[i];
            count--;

        }
        return (min == Integer.MAX_VALUE) ? -1 : min;
    }
}

```
