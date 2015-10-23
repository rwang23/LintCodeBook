##Unique Paths II

27% Accepted

####Follow up for "Unique Paths":

	Now consider if some obstacles are added to the grids. How many unique paths would there be?

	An obstacle and empty space is marked as 1 and 0 respectively in the grid.

	Have you met this question in a real interview? Yes
	Example
	For example,
	There is one obstacle in the middle of a 3x3 grid as illustrated below.

	[
	  [0,0,0],
	  [0,1,0],
	  [0,0,0]
	]
	The total number of unique paths is 2.

####Note
- m and n will be at most 100.

####Tags Expand
- Dynamic Programming
- Array

####思路
- 此题就是Uniquue-Paths变形
- 只需要添加限制条件即可
- 不要忘了初始化也有限制条件

```java
public class Solution {
    /**
     * @param obstacleGrid: A list of lists of integers
     * @return: An integer
     */
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        // write your code here
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] sum = new int[m][n];
        for (int i = 0; i < m && obstacleGrid[i][0] != 1; i++) {
            sum[i][0] = 1;
        }
        for (int i = 0; i < n && obstacleGrid[0][i] != 1; i++) {
            sum[0][i] = 1;
        }


        for (int i = 1; i < m; i++) {
            for (int j = 1; j< n; j++) {
                if( obstacleGrid[i][j] == 1) {
                    sum[i][j] = 0;
                } else {
                    sum[i][j] = sum[i - 1][j] + sum[i][j - 1];
                }
            }
        }
        return sum[m-1][n-1];
    }
}

```
