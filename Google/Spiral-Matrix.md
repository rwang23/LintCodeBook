##Spiral Matrix

	Given a matrix of m x n elements (m rows, n columns),
	return all elements of the matrix in spiral order.

	Have you met this question in a real interview? Yes
	Example
	Given the following matrix:

	[
	 [ 1, 2, 3 ],
	 [ 4, 5, 6 ],
	 [ 7, 8, 9 ]
	]
	You should return [1,2,3,6,9,8,7,4,5].

####Tags Expand
Array Matrix


####思路
- [来源](https://www.youtube.com/watch?v=siKFOI8PNKM)
- 考察下标的运算,设置一个基本值,然后通过ij变化去求值

```java
public class Solution {
    /**
     * @param matrix a matrix of m x n elements
     * @return an integer list
     */
    public List<Integer> spiralOrder(int[][] matrix) {
        // Write your code here
        if(matrix.length == 0) {
             return new ArrayList<Integer>();
        }

        List<Integer> result = new ArrayList<Integer>();
        // Initialize our four indexes
        int top = 0;
        int down = matrix.length - 1;
        int left = 0;
        int right = matrix[0].length - 1;

        while (true) {
            // Print top row
            for (int j = left; j <= right; ++j) {
                result.add(matrix[top][j]);
            }
            top++;
            if (top > down || left > right) break;

            //Print the rightmost column
            for (int i = top; i <= down; ++i) {
                result.add(matrix[i][right]);
            }
            right--;
            if (top > down || left > right) break;

            //Print the bottom row
            for (int j = right; j >= left; --j) {
                result.add(matrix[down][j]);
            }
            down--;
            if (top > down || left > right) break;

            //Print the leftmost column
            for (int i = down; i >= top; --i) {
                result.add(matrix[i][left]);
            }
            left++;
            if(top > down || left > right) break;
        }

        return result;
    }
}
```
