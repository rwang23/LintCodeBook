##3 Sum Closest

29% Accepted

	Given an array S of n integers,
    find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers.

	Have you met this question in a real interview? Yes
	Example
	For example, given array S = {-1 2 1 -4}, and target = 1. The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

	Note
	You may assume that each input would have exactly one solution.

####Challenge
O(n^2) time, O(1) extra space

####Tags Expand
Two Pointers Sort Array

####思路
- 跟3 SUM差不多


```java
public class Solution {
    /**
     * @param numbers: Give an array numbers of n integer
     * @param target : An integer
     * @return : return the sum of the three integers, the sum closest target.
     */
    public int threeSumClosest(int[] numbers ,int target) {
        // write your code here
        if (numbers == null || numbers.length < 3) {
            return Integer.MAX_VALUE;
        }
        Arrays.sort(numbers);
        int sum = numbers[0] + numbers[1] + numbers[2];
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < numbers.length - 2; i++) {
            int find = target - numbers[i];
            int start = i + 1;
            int end = numbers.length - 1;
            while (start < end) {
                if (numbers[start] + numbers[end] > find) {
                    int cur = numbers[i] + numbers[start] + numbers[end];
                    min = Math.min(cur - target, min);
                    if (min == cur - target) {
                        sum = cur;
                    }
                    end--;
                } else if (numbers[start] + numbers[end] < find) {
                    int cur = numbers[i] + numbers[start] + numbers[end];
                    min = Math.min(target - cur, min);
                    if (min == target - cur) {
                        sum = cur;
                    }
                    start++;
                } else {
                    return target;
                }
            }
        }
        return sum;
    }
}


```
