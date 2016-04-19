##Missing Number

	Total Accepted: 40211 Total Submissions: 102474 Difficulty: Medium
	Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

	For example,
	Given nums = [0, 1, 3] return 2.

	Note:
	Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

####思路
- 我的慢速做法
- 虽然也是O(n) 但是明显比别人的慢

```java
public class Solution {

    public int missingNumber(int[] nums) {

        int n = nums.length;
        HashSet<Integer> set = new HashSet<Integer>();

        int min = 0;
        int max = 0;
        for (int i = 0; i < n; i++) {
            set.add(nums[i]);
            min = Math.min(nums[i], min);
            max = Math.max(nums[i], max);
        }

        int start = min;

        while (min < max) {
            if (set.contains(min)) {
                set.remove(min++);
            } else {
                return min;
            }
        }

        return max + 1;
    }
}
```

####Bits Manipulation超简单做法
- Xor大法, 把0 - n 都xor起来
- 再xor数组里的,剩下的就是答案

```java
public int missingNumber(int[] nums) {

    int xor = 0, i = 0;
    for (i = 0; i < nums.length; i++) {
        xor = xor ^ i ^ nums[i];
    }

    return xor ^ i;
}
```

####Sum 大法
- 求和,0-n加起来,再减数组的
- 不过由于是加法,所以考虑如果len很大,sum可以用long类型

```java
public int missingNumber(int[] nums) { //sum
    int len = nums.length;
    int sum = (0+len)*(len+1)/2;
    for(int i=0; i<len; i++)
        sum-=nums[i];
    return sum;
}
```
