##Search a 2D Matrix

27% Accepted

    Write an efficient algorithm that searches for a value in an m x n matrix.

    This matrix has the following properties:
    - Integers in each row are sorted from left to right.
    - The first integer of each row is greater than the last integer of the previous row.

	Consider the following matrix:

	[
	    [1, 3, 5, 7],
	    [10, 11, 16, 20],
	    [23, 30, 34, 50]
	]
	Given target = 3, return true.


####Challenge
O(log(n) + log(m)) time

####Tags Expand
- Binary Search
- Matrix

####思路
- 两次二分搜索


```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        int start = 0;
        int end = m - 1;
        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (matrix[mid][0] == target) {
                return true;
            }
            else if (matrix[mid][0] > target) {
                end = mid;
            }
            else {
                start = mid;
            }
        }

        int row = (matrix[end][0] <= target) ? end : start;

        start = 0;
        end = n - 1;
        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (matrix[row][mid] == target) {
                return true;
            }
            else if (matrix[row][mid] > target) {
                end = mid;
            }
            else {
                start = mid;
            }
        }

        return (matrix[row][start] == target || matrix[row][end] == target);
    }
}
```
