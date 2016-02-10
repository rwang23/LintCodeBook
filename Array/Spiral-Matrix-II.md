##Spiral Matrix II


	Given an integer n, generate a square matrix filled with elements from 1 to n^2 in spiral order.

	Have you met this question in a real interview? Yes
	Example
	Given n = 3,

	You should return the following matrix:

	[
	  [ 1, 2, 3 ],
	  [ 8, 9, 4 ],
	  [ 7, 6, 5 ]
	]

####Tags Expand
Array

####思路
- 跟spiral matrix I 一样

```java
public class Solution {
    /**
     * @param n an integer
     * @return a square matrix
     */
    public int[][] generateMatrix(int n) {
        // Write your code here
        if (n <= 0) {
            return new int[0][0];
        }

        int[][] result = new int[n][n];

        int top = 0;
        int down = n - 1;
        int left = 0;
        int right = n - 1;
        int num = 1;

        while (true) {
            // Print top row
            for (int j = left; j <= right; ++j) {
                result[top][j] = num++;;
            }
            top++;
            if (top > down || left > right) break;

            //Print the rightmost column
            for (int i = top; i <= down; ++i) {
                result[i][right] = num++;
            }
            right--;
            if (top > down || left > right) break;

            //Print the bottom row
            for (int j = right; j >= left; --j) {
                result[down][j] = num++;
            }
            down--;
            if (top > down || left > right) break;

            //Print the leftmost column
            for (int i = down; i >= top; --i) {
                result[i][left] = num++;
            }
            left++;
            if(top > down || left > right) break;
        }

        return result;
    }
}
```
