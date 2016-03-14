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

    private class Node{
        int x;
        int y;
        Node(int x, int y) {
            this.x = x;
            this.y = y;
        }
    }

    public int numIslands(boolean[][] grid) {
        int m = grid.length;
        if (m == 0) {
            return 0;
        }
        int n = grid[0].length;
        if (n == 0) {
            return 0;
        }

        int[][] isVisited = new int[m][n];
        int count = 0;
        int[] xstep = new int[]{0, 1, -1, 0};
        int[] ystep = new int[]{1, 0, 0, -1};
        Queue<Node> queue = new LinkedList<Node>();


        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == false || isVisited[i][j] == 1) {
                    continue;
                }
                Node cur = new Node(i, j);
                queue.offer(cur);
                count++;

                while (!queue.isEmpty()) {

                    cur = queue.poll();
                    for (int s = 0; s < 4; s++) {
                        int nextX = cur.x + xstep[s];
                        int nextY = cur.y + ystep[s];
                        if (nextX < m && nextY < n && nextY >= 0 && nextX >= 0 && grid[nextX][nextY] == true && isVisited[nextX][nextY] == 0) {
                            isVisited[nextX][nextY] = 1;
                            Node next = new Node(nextX, nextY);
                            queue.offer(next);
                        }
                    }

                }
            }
        }
        return count;
    }
}
```
