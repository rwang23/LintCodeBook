##Maximal Square

24% Accepted

    Given a 2D binary matrix filled with 0's and 1's,
    find the largest square containing all 1's and return its area.

    Have you met this question in a real interview? Yes
    Example
    For example, given the following matrix:

    1 0 1 0 0
    1 0 1 1 1
    1 1 1 1 1
    1 0 0 1 0
    Return 4.

####Tags Expand
- Dynamic Programming

####思路
- 画图自己找的规律

####矩阵图
a=16 b=25

    [0,1,1,1,1,1,1,1,1,1]
    [1,0,1,1,1,1,1,1,1,1]
    [1,1,0,1,1,1,1,1,1,1]
    [1,1,1,0,1,1,1,1,1,1]
    [1,1,1,1,0,1,1,1,1,1]
    [1,1,1,1,1,0,1,1,1,1]
    [1,1,1,1,1,1,0,1,1,1]
    [1,1,1,1,1,1,1,0,1,1]
    [1,1,1,1,1,1,1,1,0,1]
    [1,1,1,1,1,1,1,1,1,0]

    [0,1,1,1,1,1,1,1,1,1]
    [1,0,1,4,4,4,4,4,4,4]
    [1,1,0,1,4,9,9,9,9,9]
    [1,4,1,0,1,4,9,a,a,a]
    [1,4,4,1,0,1,4,9,a,b]
    [1,4,9,4,1,0,1,4,9,a]
    [1,4,1,1,1,1,0,1,1,1]
    [1,1,1,1,1,1,1,0,1,1]
    [1,1,1,1,1,1,1,1,0,1]
    [1,1,1,1,1,1,1,1,1,0]

```java
public class Solution {
    public int maxSquare(int[][] matrix) {
        if (matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] area = new int[m][n];
        int maxArea = 0;
        for (int i = 0; i < m; i++) {
            area[i][0] = matrix[i][0];
            maxArea = Math.max(maxArea,area[i][0]);
        }
        for (int j = 0; j < n; j++) {
            area[0][j] = matrix[0][j];
            maxArea = Math.max(maxArea,area[0][j]);
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i-1][j-1] == 1 && matrix[i-1][j] == 1 && matrix[i][j-1] == 1 && matrix[i][j] == 1) {
                    int min = Math.min(Math.min(area[i-1][j-1], area[i-1][j]), area[i][j-1]);
                    Double big = (int)(Math.sqrt(min) + 1) * (Math.sqrt(min) + 1);
                    area[i][j] = big.intValue();
                    maxArea = Math.max(maxArea,area[i][j]);
                } else {
                    area[i][j] = matrix[i][j];
                }
            }
        }
        return maxArea;
    }
}

```
