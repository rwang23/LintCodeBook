##Burst Balloons

	Total Accepted: 7090 Total Submissions: 19887 Difficulty: Hard
	Given n balloons, indexed from 0 to n-1.
	Each balloon is painted with a number on it represented by array nums.
	You are asked to burst all the balloons.
	If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins.
	Here left and right are adjacent indices of i.
	After the burst, the left and right then becomes adjacent.

	Find the maximum coins you can collect by bursting the balloons wisely.

	Note:
	(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
	(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

	Example:

	Given [3, 1, 5, 8]

	Return 167

	    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
	   coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167

####思路
- 像树一样,蹭蹭递归,所以想到用DFS,但是超时了

```java
public class Solution {
    int max = 0;
    public int maxCoins(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(1);
        for (int i = 0; i < nums.length; i++) {
            list.add(nums[i]);
        }
        list.add(1);

        dfs(list, 0);
        return max;
    }

    public void dfs(ArrayList<Integer> list, int sum) {
        int n = list.size();
        if (n == 3) {
            sum += list.get(1);
            max = Math.max(max, sum);
            return;
        }

        for (int i = 1; i < n - 1; i++) {
            int temp = list.get(i - 1) * list.get(i) * list.get(i + 1);
            int cur = list.get(i);
            sum += temp;
            list.remove(i);
            dfs(list, sum);
            sum -= temp;
            list.add(i, cur);
        }

    }
}
```

####分治法
[参考](http://algobox.org/burst-balloons/)

```java
public int maxCoins(int[] iNums) {
    int[] nums = new int[iNums.length + 2];
    int n = 1;
    for (int x : iNums) if (x > 0) nums[n++] = x;
    nums[0] = nums[n++] = 1;


    int[][] memo = new int[n][n];
    return burst(memo, nums, 0, n - 1);
}

public int burst(int[][] memo, int[] nums, int left, int right) {
    if (left + 1 == right) return 0;
    if (memo[left][right] > 0) return memo[left][right];
    int ans = 0;
    for (int i = left + 1; i < right; ++i)
        ans = Math.max(ans, nums[left] * nums[i] * nums[right]
        + burst(memo, nums, left, i) + burst(memo, nums, i, right));
    memo[left][right] = ans;
    return ans;
}
```

####动规
[参考](http://algobox.org/burst-balloons/)


```java
public int maxCoins(int[] iNums) {
    int[] nums = new int[iNums.length + 2];
    int n = 1;
    for (int x : iNums) if (x > 0) nums[n++] = x;
    nums[0] = nums[n++] = 1;


    int[][] dp = new int[n][n];
    for (int k = 2; k < n; ++k)
        for (int left = 0; left < n - k; ++left) {
            int right = left + k;
            for (int i = left + 1; i < right; ++i)
                dp[left][right] = Math.max(dp[left][right],
                nums[left] * nums[i] * nums[right] + dp[left][i] + dp[i][right]);
        }

    return dp[0][n - 1];
}
```
