##Best Meeting Point

	Total Accepted: 3540 Total Submissions: 7703 Difficulty: Hard
	A group of two or more people wants to meet and minimize the total travel distance. You are given a 2D grid of values 0 or 1, where each 1 marks the home of someone in the group. The distance is calculated using Manhattan Distance, where distance(p1, p2) = |p2.x - p1.x| + |p2.y - p1.y|.

	For example, given three people living at (0,0), (0,4), and (2,2):

	1 - 0 - 0 - 0 - 1
	|   |   |   |   |
	0 - 0 - 0 - 0 - 0
	|   |   |   |   |
	0 - 0 - 1 - 0 - 0
	The point (0,2) is an ideal meeting point, as the total travel distance of 2+2+2=6 is minimal. So return 6.

####思路
- 暴力O(mnk)

```java
public class Solution {
    class Point{
        private int x;
        private int y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public int minTotalDistance(int[][] grid) {
        int m = grid.length;
        if (m == 0) {
            return 0;
        }
        int n = grid[0].length;
        if (n == 0) {
            return 0;
        }

        List<Point> homes = new ArrayList<Point>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    homes.add(new Point(i, j));
                }
            }
        }
        int min = Integer.MAX_VALUE;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int distance = 0;
                for (int k = 0; k < homes.size(); k++) {
                    Point meetPoint = homes.get(k);
                    distance += (Math.abs(meetPoint.x - i) + Math.abs(meetPoint.y - j));
                }
                min = Math.min(min, distance);
            }
        }
        return min;
    }
}
```

####优化
[dietpepsi](http://algobox.org/best-meeting-point/)

```java
public class Solution {
    public int minTotalDistance(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[] row_sum = new int[n], col_sum = new int[m];
        for (int i = 0; i < m; ++i)
            for (int j = 0; j < n; ++j) {
                row_sum[j] += grid[i][j];
                col_sum[i] += grid[i][j];
            }
        return minDistance1D(row_sum) + minDistance1D(col_sum);
    }

    public int minDistance1D(int[] vector) {
        int i = -1, j = vector.length;
        int d = 0, left = 0, right = 0;
        while (i != j) {
            if (left < right) {
                d += left;
                left += vector[++i];
            } else {
                d += right;
                right += vector[--j];
            }
        }
        return d;
    }
}
```
