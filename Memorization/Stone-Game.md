##Stone Game

	There is a stone game.At the beginning of the game the player picks n piles of stones in a line.

	The goal is to merge the stones in one pile observing the following rules:

	At each step of the game,the player can merge two adjacent piles to a new pile.
	The score is the number of stones in the new pile.
	You are to determine the minimum of the total score.

	Have you met this question in a real interview? Yes
	Example
	Tags
	Related Problems
	 Notes
	For [4, 1, 1, 4], in the best solution, the total score is 18:

	1. Merge second and third piles => [4, 2, 4], score +2
	2. Merge the first two piles => [6, 4]，score +6
	3. Merge the last two piles => [10], score +10
	Other two examples:
	[1, 1, 1, 1] return 8
	[4, 4, 5, 9] return 43

####思路
- Memorization: DFS + 动态规划
- 区间型动态规划

```java
public class Solution {
    /**
     * @param A an integer array
     * @return an integer
     */
    public int stoneGame(int[] A) {
        // Write your code here
        if (A == null || A.length == 0) {
            return 0;
        }

        int n = A.length;
        int[][] dp = new int[n][n];
        int[] sum = new int[n + 1];

        for (int i = 1; i <= n; i++) {
            sum[i] =  sum[i - 1] + A[i - 1];
        }

        return dfs(A, dp, 0, n - 1, sum);
    }

    public int dfs(int[] A, int[][] dp, int start, int end, int[] sum) {
        if (start == end) {
            return 0;
        }

        if (dp[start][end] != 0) {
            return dp[start][end];
        }


        int min = Integer.MAX_VALUE;
        for (int i = start; i < end; i++) {
            int left = dfs(A, dp, start, i, sum);
            int right = dfs(A, dp, i + 1, end, sum);
            min = Math.min(min, left + right);
        }

        dp[start][end] = min + sum[end + 1] - sum[start];

        return dp[start][end];
    }
}

```
