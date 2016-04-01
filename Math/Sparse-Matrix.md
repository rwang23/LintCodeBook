##Sparse Matrix
	Total Accepted: 5033 Total Submissions: 10671 Difficulty: Medium
	Given two sparse matrices A and B, return the result of AB.

	You may assume that A's column number is equal to B's row number.

	Example:

	A = [
	  [ 1, 0, 0],
	  [-1, 0, 3]
	]

	B = [
	  [ 7, 0, 0 ],
	  [ 0, 0, 0 ],
	  [ 0, 0, 1 ]
	]


	     |  1 0 0 |   | 7 0 0 |   |  7 0 0 |
	AB = | -1 0 3 | x | 0 0 0 | = | -7 0 3 |
	                  | 0 0 1 |

####思路
- 直接矩阵乘法 O(mkn),不能通过test case

```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        int m1 = A.length;
        int n1 = A[0].length;
        int m2 = B.length;
        int n2 = B[0].length;

        int[][] result = new int[m1][n2];

        for (int i = 0; i < m1; i++) {
            for (int j = 0; j < n1; j++) {
                for (int k = 0; k < n2; k++) {
                    result[i][k] += A[i][j] * B[j][k];
                }

            }
        }

        return result;
    }
}
```

####优化
- 根据sparse 特性,稍微优化
- 先固定A中的元素,如果这个元素是0,那么跟这个元素相关的运算都可以忽略了

```java
public class Solution {
    public int[][] multiply(int[][] A, int[][] B) {
        int m1 = A.length;
        int n1 = A[0].length;
        int m2 = B.length;
        int n2 = B[0].length;

        int[][] result = new int[m1][n2];

        for (int i = 0; i < m1; i++) {
            for (int j = 0; j < n1; j++) {
                if (A[i][j] != 0) {
                    for (int k = 0; k < n2; k++) {
                        result[i][k] += A[i][j] * B[j][k];
                    }
                }

            }
        }

        return result;
    }
}
```
