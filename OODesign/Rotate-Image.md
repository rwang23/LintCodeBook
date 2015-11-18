##Rotate Image

35% Accepted

	You are given an n x n 2D matrix representing an image.
	Rotate the image by 90 degrees (clockwise).

	Have you met this question in a real interview? Yes
	Example
	Given a matrix

	[
	    [1,2],
	    [3,4]
	]
	rotate it by 90 degrees (clockwise), return

	[
	    [3,1],
	    [4,2]
	]

####Challenge
Do it in-place.

####Tags Expand
Cracking The Coding Interview Matrix

####思路
- 简单硬做题
- 再申请一个辅助数组就很好做,直接保存,但是题意挑战让原地做
- 如果进行原地,就是替换一个值,然后要继续替换替换的这个值的位置
- 画图,把整个矩阵遍历完,通过ij两重循环以及while来做的
- 时间O(n)

```java
public class Solution {
    /**
     * @param matrix: A list of lists of integers
     * @return: Void
     */
    public void rotate(int[][] matrix) {
        // write your code here
        if (matrix == null || matrix.length == 0) {
            return ;
        }
        int m = matrix.length;
        if (matrix[0] == null || matrix[0].length == 0) {
            return ;
        }
        int n = matrix[0].length;

        if (m != n) {
            return ;
        }

        for (int i = 0; i < n / 2; i++) {
            for (int j = i; j < n - i - 1; j++) {
                int local = matrix[i][j];
                int count = 0;
                while (count < 4) {
                    int newX = j;
                    int newY = (n - 1) - i;
                    int temp = matrix[newX][newY];
                    matrix[newX][newY] = local;
                    i = newX;
                    j = newY;
                    local = temp;
                    count++;
                }
            }
        }

    }
}

```
