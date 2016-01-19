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

####空间优化做法
- 优化f[i][j]到f[j]
- 此时第二重循环不能从j=0开始了，要从j=m开始 j--
- 如果是j=0 j++开始，那么f[j-A[i-1]]用的就是新的值，不是原来的f[i-1][j-A[i-1]]而是刚计算完的f[1] f[2]这样


```java
public class Solution {

    public int backPack(int m, int[] A) {
        // write your code here
        if (m ==0 || A == null || A.length == 0) {
            return 0;
        }
        int[] f = new int[m+1];
        f[0] = 0;
        for (int i = 1; i <= A.length; i++) {
            for (int j = m; j >= 0; j--) {
                if (j >= A[i-1]) {
                    f[j] = Math.max(f[j-A[i-1]] + V[i-1], f[j]);
                }
            }
        }
        return f[m];
    }
}

```

####更好理解的空间优化做法
```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A & V: Given n items with size A[i] and value V[i]
     * @return: The maximum value
     */
    public int backPackII(int m, int[] A, int V[]) {
        // write your code here
        if (m <= 0 || A == null || V == null) {
            return 0;
        }

        int n = A.length;
        int[][] result = new int[2][m+1];
        for (int i = 0; i <= m; i++) {
            result[0][i] = 0;
        }
        for (int i = 0; i <= 1; i++) {
            result[i][0] = 0;
        }

        for (int i = 1; i <= n; i++) {
            for (int j = m; j >= 0; j--) {
                if (j - A[i-1] >= 0) {
                    result[i%2][j] = Math.max(result[(i-1)%2][j], result[(i-1)%2][j-A[i-1]] + V[i-1]);
                } else {
                    result[i%2][j] = result[(i-1)%2][j];
                }
            }
        }

        return result[A.length%2][m];
    }
}
```
