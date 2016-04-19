##Set Matrix Zeroes
	Total Accepted: 63087 Total Submissions: 189695 Difficulty: Medium
	Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

	click to show follow up.

	Follow up:
	Did you use extra space?
	A straight forward solution using O(mn) space is probably a bad idea.
	A simple improvement uses O(m + n) space, but still not the best solution.
	Could you devise a constant space solution?

####思路
- 首先想到了O(m+n) space方法

```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        List<Integer> zeroX = new ArrayList<Integer>();
        List<Integer> zeroY = new ArrayList<Integer>();

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == 0) {
                    zeroX.add(i);
                    zeroY.add(j);
                }
            }
        }

        for (int k = 0; k < zeroX.size(); k++) {
            for (int i = 0; i < n; i++) {
                matrix[zeroX.get(k)][i] = 0;
            }
            for (int i = 0; i < m; i++) {
                matrix[i][zeroY.get(k)] = 0;
            }
        }
    }
}
```

####优化 Constant place
- 如果某个点(x, y).value==0,那么设置这个点 (x,0) = 0, (0, y) = 0
- 初始化完一遍之后,然后再整理一遍

```java
public class Solution {
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }

        int m = matrix.length;
        int n = matrix[0].length;
        boolean firstRow = false;
        boolean firstCol = false;

        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstCol = true;
                break;
            }
        }

        for (int i = 0; i < n; i++) {
            if (matrix[0][i] == 0) {
                firstRow = true;
                break;
            }
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for (int i = 1; i < m; i++) {
            if (matrix[i][0] == 0) {
                for (int j = 0; j < n; j++) {
                    matrix[i][j] = 0;
                }
            }
        }

        for (int i = 1; i < n; i++) {
            if (matrix[0][i] == 0) {
                for (int j = 0; j < m; j++) {
                    matrix[j][i] = 0;
                }
            }
        }

        if (firstRow) {
            for (int i = 0; i < n; i++) {
                matrix[0][i] = 0;
            }
        }
        if (firstCol) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }

    }
}
```
