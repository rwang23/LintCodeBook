##Triangle

	26% Accepted
	Given a triangle, find the minimum path sum from top to bottom.
    Each step you may move to adjacent numbers on the row below.

	Have you met this question in a real interview? Yes
	Example
	For example, given the following triangle

	[
	     [2],
	    [3,4],
	   [6,5,7],
	  [4,1,8,3]
	]
	The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

####Note
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

####Tags Expand
- Dynamic Programming


----

####bottom-up动态规划
```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers.
     * @return: An integer, minimum path sum.
     */
    public int minimumTotal(ArrayList<ArrayList<Integer>> triangle) {
        // write your code here
        int n = triangle.size();
        int[][] sum = new int[n][n];

        for (int i = 0; i < n; i++) {
            sum[n-1][i] = triangle.get(n-1).get(i).intValue();
        }

        for ( int i = n - 2; i >= 0; i--) {
            for (int j = 0; j <= i; j++  ) {
                int root = triangle.get(i).get(j).intValue();
                sum[i][j] =root + Math.min(sum[i+1][j], sum[i+1][j+1]);
            }
        }

        return sum[0][0];
    }


}

```

####分治法
```java
public class Solution {
    /**
     * @param triangle: a list of lists of integers.
     * @return: An integer, minimum path sum.
     */
    public int minimumTotal(ArrayList<ArrayList<Integer>> triangle) {
        // write your code here
        return divideconquer(0, 0, triangle);
    }

    public int divideconquer(int x, int y, ArrayList<ArrayList<Integer>> triangle){
        if (y == triangle.size() || x == triangle.size()) {
            return 0;
        }
        int min = Math.min(divideconquer(x,y+1,triangle),divideconquer(x+1,y+1,triangle));
        return min + triangle.get(y).get(x).intValue();
    }


}
```
