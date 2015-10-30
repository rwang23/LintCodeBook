##Backpack II

34% Accepted

	Given n items with size Ai and value Vi, and a backpack with size m.
	What's the maximum value can you put into the backpack?

	Example
	Given 4 items with size [2, 3, 5, 7] and value [1, 5, 2, 4], and a backpack with size 10. The maximum value is 9.

####Note
You cannot divide item into small pieces and the total size of items you choose should smaller or equal to m.

####Challenge
O(n x m) memory is acceptable, can you do it in O(m) memory?

####Tags Expand
- LintCode Copyright
- Dynamic Programming
- Backpack

####基本做法
- - 参考 背包九讲
- f[i][j] = Math.max(f[i-1][j-A[i-1]] + V[i-1], f[i-1][j])

```java
public class Solution {
    public int backPackII(int m, int[] A, int V[]) {
        if (m ==0 || A == null || A.length == 0 || V == null || A.length != V.length) {
            return 0;
        }
        int[][] f = new int[A.length+1][m+1];
        for (int i = 0; i <= m; i++) {
            f[0][i] = 0;
        }
        for (int i = 1; i <= A.length; i++) {
            for (int j = 0; j <= m; j++) {
                if (j >= A[i-1]) {
                    f[i][j] = Math.max(f[i-1][j-A[i-1]] + V[i-1], f[i-1][j]);
                } else {
                    f[i][j] = f[i-1][j];
                }
            }
        }
        return f[A.length][m];
    }
}

```
