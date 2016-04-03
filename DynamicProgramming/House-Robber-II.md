##House Robber II
	Total Accepted: 25571 Total Submissions: 84355 Difficulty: Medium
	Note: This is an extension of House Robber.

	After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention.
	This time, all houses at this place are arranged in a circle.
	That means the first house is the neighbor of the last one.
	Meanwhile, the security system for these houses remain the same as for those in the previous street.

	Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

####思路
- 分成两个部分:去不去第一个家
- 第一个可能性是去第一个家,去了那么最后一个一定不能去
- 第二个可能性是不去第一个,那么有可能取最后一个
- 就是初始化的时候有点变化

```java
public class Solution {
/*
take 0 then not take len - 1
not take 0 then may take len - 1

f[i] = Math.max(f[i - 1], f[i - 2] + nums[i])

take 0
start f[i] from i = 2, because i = 0 take and i = 1 not take
f[0] = nums[0], f[1] = f[0]
end at f[n - 2]
return f[n - 2]

not take 0,
start at i = 0,
f[0] = 0, f[1] = nums[1]
return f[n - 1]

*/
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int len = nums.length;
        if (len == 1) {
            return nums[0];
        }
        int[] robProfits = new int[len];

        int max = 0;
        //first calculate take 0
        robProfits[0] = nums[0];
        robProfits[1] = robProfits[0];
        for (int i = 2; i < len - 1; i++) {
            robProfits[i] = Math.max(robProfits[i - 1], robProfits[i - 2] + nums[i]);
        }
        max = robProfits[len - 2];

        //then calcuate not take 0
        robProfits[0] = 0;
        robProfits[1] = nums[1];
        for (int i = 2; i < len; i++) {
            robProfits[i] = Math.max(robProfits[i - 1], robProfits[i - 2] + nums[i]);
        }
        max = Math.max(max, robProfits[len - 1] );

        return max;
    }
}
```
