##Number of Islands

19% Accepted

	Given a boolean 2D matrix, find the number of islands.

	Have you met this question in a real interview? Yes
	Example
	Given graph:

	[
	  [1, 1, 0, 0, 0],
	  [0, 1, 0, 0, 1],
	  [0, 0, 0, 1, 1],
	  [0, 0, 0, 0, 0],
	  [0, 0, 0, 0, 1]
	]
	return 3.

####Note
0 is represented as the sea, 1 is represented as the island.
If two 1 is adjacent, we consider them in the same island.
We only consider up/down/left/right adjacent.

####思路
- DFS方法
- 只要遍历一遍，碰到一个1，就把它周围所有相连的1都标记为非1，这样整个遍历过程中碰到的1的个数就是所求解。

```java
public class Solution {
    /**
     * @param grid a boolean 2D matrix
     * @return an integer
     */
    private int m, n;
    public int numIslands(boolean[][] grid) {
        m = grid.length;
        if (m == 0) return 0;
        n = grid[0].length;
        if (n == 0) return 0;

        int sum = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] != true) continue;

                sum++;
                dfs(grid, i, j);
            }
        }
        return sum;
    }


    public void dfs(boolean[][] grid, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n) {
            return;
        }

        if (grid[i][j] == true) {
            grid[i][j] = false;
            dfs(grid, i - 1, j);
            dfs(grid, i + 1, j);
            dfs(grid, i, j - 1);
            dfs(grid, i, j + 1);
        }
    }
}

```

####BFS

```java
public class Solution {
    /**
     * @param grid: a boolean 2D matrix
     * @return: an integer
     */

    public class Point {
        int x;
        int y;
        Point(int x, int y) {
            this.x = x;
            this.y = y;
        }


    }
    public int numIslands(boolean[][] grid) {
        // write your code here
        if (grid == null || grid.length == 0 || grid[0] == null || grid[0].length == 0) {
            return 0;
        }

        boolean[][] visited = new boolean[grid.length][grid[0].length];
        Queue<Point> queue = new LinkedList<Point>();
        int total = 0;

        for (int i = 0; i < grid.length; i ++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (!visited[i][j] && grid[i][j]) {
                    queue.offer(new Point(i, j));
                    visited[i][j] = true;
                    bfs(queue, visited, grid);
                    total++;
                }
            }
        }

        return total;
    }

    public void bfs(Queue<Point> queue, boolean[][] visited, boolean[][] grid) {

        int[] directionX = {-1, 0, 0, 1};
        int[] directionY = {0, -1, 1, 0};

        while (!queue.isEmpty()) {

            Point cur = queue.poll();
            for (int i = 0; i < 4; i++) {
                int x = cur.x + directionX[i];
                int y = cur.y + directionY[i];
                if (x < grid.length && x >= 0 && y < grid[0].length && y >= 0)
                    if (!visited[x][y] && grid[x][y]) {
                        queue.offer(new Point(x, y));
                        visited[x][y] = true;
                    }
                }
            }
        }

    }


```
