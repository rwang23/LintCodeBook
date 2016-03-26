##Paint House

	Total Accepted: 6852 Total Submissions: 16252 Difficulty: Medium
	There are a row of n houses, each house can be painted with one of the three colors: red, blue or green.
	The cost of painting each house with a certain color is different.
	You have to paint all the houses such that no two adjacent houses have the same color.

	The cost of painting each house with a certain color is represented by a n x 3 cost matrix.
	For example, costs[0][0] is the cost of painting house 0 with color red; costs[1][2] is the cost of painting house 1 with color green, and so on...
	Find the minimum cost to paint all houses.

	Note:
	All costs are positive integers.

####思路
- 设置三个DP数组,分别表示涂一个颜色
-           R[i] = Math.min(B[i - 1], G[i - 1]) + cost[i][0];
            B[i] = Math.min(R[i - 1], G[i - 1]) + cost[i][1];
            G[i] = Math.min(B[i - 1], R[i - 1]) + cost[i][2];

```java
public class Solution {
    public int minCost(int[][] cost) {
        if (cost == null || cost.length == 0 || cost[0].length == 0) {
            return 0;
        }

        int n = cost.length;
        int[] R = new int[n];
        int[] B = new int[n];
        int[] G = new int[n];

        R[0] = cost[0][0];
        B[0] = cost[0][1];
        G[0] = cost[0][2];

        for (int i = 1; i < n; i++) {
            R[i] = Math.min(B[i - 1], G[i - 1]) + cost[i][0];
            B[i] = Math.min(R[i - 1], G[i - 1]) + cost[i][1];
            G[i] = Math.min(B[i - 1], R[i - 1]) + cost[i][2];
        }

        return Math.min(R[n - 1], Math.min(B[n - 1], G[n - 1]));
    }
}
```
