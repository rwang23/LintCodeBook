##Backpack

19% Accepted

	Given n items with size Ai, an integer m denotes the size of a backpack.
	How full you can fill this backpack?

	If we have 4 items with size [2, 3, 5, 7], the backpack size is 11, we can select [2, 3, 5],
	so that the max size we can fill this backpack is 10. If the backpack size is 12.
	we can select [2, 3, 7] so that we can fulfill the backpack.

	You function should return the max size we can fill in the given backpack.

####Note
You can not divide any item into small pieces.

####Challenge
- O(n x m) time and O(m) memory.
- O(n x m) memory is also acceptable if you do not know how to optimize memory.

####Tags Expand
- LintCode Copyright
- Dynamic Programming
- Backpack

####基本做法
- Space O(m*n) 因为每次就在用f[i] f[i-1] 所以应该空间是可以优化的
- Time O(m*n)
- 参考 背包九讲
- f[i][j] = Math.max(f[i-1][j-A[i-1]] + V[i-1], f[i-1][j])

```java
public class Solution {

    public int backPack(int m, int[] A) {
        // write your code here
        if (m ==0 || A == null || A.length == 0) {
            return 0;
        }
        int[][] f = new int[A.length+1][m+1];
        for (int i = 0; i <= m; i++) {
            f[0][i] = 0;
        }
        for (int i = 1; i <= A.length; i++) {
            for (int j = 0; j <= m; j++) {
                if (j >= A[i-1]) {
                    f[i][j] = Math.max(f[i-1][j-A[i-1]] + A[i-1], f[i-1][j]);
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
                    f[j] = Math.max(f[j-A[i-1]] + A[i-1], f[j]);
                }
            }
        }
        return f[m];
    }
}

```
####或者这样更好理解
```java
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        // write your code here
        if (m <= 0 || A == null) {
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
                    result[i%2][j] = Math.max(result[(i-1)%2][j], result[(i-1)%2][j-A[i-1]] + A[i-1]);
                } else {
                    result[i%2][j] = result[(i-1)%2][j];
                }
            }
        }

        return result[A.length%2][m];
    }
}
```
