##Walls and Gates

	Total Accepted: 7828 Total Submissions: 21206 Difficulty: Medium
	You are given a m x n 2D grid initialized with these three possible values.

	-1 - A wall or an obstacle.
	0 - A gate.
	INF - Infinity means an empty room. We use the value 231 - 1 = 2147483647 to represent INF as you may assume that the distance to a gate is less than 2147483647.
	Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, it should be filled with INF.

	For example, given the 2D grid:
	INF  -1  0  INF
	INF INF INF  -1
	INF  -1 INF  -1
	  0  -1 INF INF
	After running your function, the 2D grid should be:
	  3  -1   0   1
	  2   2   1  -1
	  1  -1   2  -1
	  0  -1   3   4

####思路
- BFS
- 第一反应是从0入手,然后不断更新周边的距离值,O(kmn), k是gate的数量
- 但是刚开始写的时候(第一个代码),太傻了,再遍历矩阵的时候去进行bfs
- 其实如果直接把点值等于0的点全部push进queue就完了嘛,
- 就优化到了O(mn) (第二份代码基本没有改动,就稍微改变一个顺序)

```java
public class Solution {
    private class Point{
        private int x;
        private int y;
        private int distance;
        Point(int x, int y, int distance) {
            this.x = x;
            this.y = y;
            this.distance = distance;
        }
    }
    static int inf = 2147483647;
    public void wallsAndGates(int[][] rooms) {
        if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
            return;
        }
        int m = rooms.length;
        int n = rooms[0].length;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                Queue<Point> queue = new LinkedList<Point>();
                if (rooms[i][j] == 0) {
                    bfs(rooms, queue, i, j);
                }
            }
        }
    }

    public void bfs(int[][] rooms, Queue<Point> queue, int x, int y) {

        int[] xstep = new int[]{0, 0, 1, -1};
        int[] ystep = new int[]{1, -1, 0, 0};
        boolean[][] isVisited = new boolean[rooms.length][rooms[0].length];
        queue.offer(new Point(x, y, 0));
        isVisited[x][y] = true;
        while (!queue.isEmpty()) {
            Point cur = queue.poll();
            int distance = cur.distance;

            for (int i = 0; i < 4; i++) {
                int newX = cur.x + xstep[i];
                int newY = cur.y + ystep[i];
                if (newX < rooms.length && newY < rooms[0].length && newX >= 0 && newY >= 0 && rooms[newX][newY] != -1 && rooms[newX][newY] != 0 && isVisited[newX][newY] == false) {

                    rooms[newX][newY] = Math.min(rooms[newX][newY], distance + 1);

                    isVisited[newX][newY] = true;
                    queue.offer(new Point(newX, newY, rooms[newX][newY]));
                }
            }
        }

    }
}
```

####优化

```java
public class Solution {
    private class Point{
        private int x;
        private int y;
        private int distance;
        Point(int x, int y, int distance) {
            this.x = x;
            this.y = y;
            this.distance = distance;
        }
    }
    static int inf = 2147483647;
    public void wallsAndGates(int[][] rooms) {
        if (rooms == null || rooms.length == 0 || rooms[0].length == 0) {
            return;
        }
        int m = rooms.length;
        int n = rooms[0].length;
        Queue<Point> queue = new LinkedList<Point>();
        boolean[][] isVisited = new boolean[rooms.length][rooms[0].length];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (rooms[i][j] == 0) {
                    queue.offer(new Point(i, j, 0));
                    isVisited[i][j] = true;
                }
            }
        }
        bfs(rooms, queue, isVisited);
    }

    public void bfs(int[][] rooms, Queue<Point> queue, boolean[][] isVisited) {

        int[] xstep = new int[]{0, 0, 1, -1};
        int[] ystep = new int[]{1, -1, 0, 0};


        while (!queue.isEmpty()) {
            Point cur = queue.poll();
            int distance = cur.distance;

            for (int i = 0; i < 4; i++) {
                int newX = cur.x + xstep[i];
                int newY = cur.y + ystep[i];
                if (newX < rooms.length && newY < rooms[0].length && newX >= 0 && newY >= 0 && rooms[newX][newY] != -1 && rooms[newX][newY] != 0 && isVisited[newX][newY] == false) {

                    rooms[newX][newY] = Math.min(rooms[newX][newY], distance + 1);
                    isVisited[newX][newY] = true;
                    queue.offer(new Point(newX, newY, rooms[newX][newY]));
                }
            }
        }

    }
}
```
