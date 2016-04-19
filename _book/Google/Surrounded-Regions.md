##Surrounded Regions
	Total Accepted: 49679 Total Submissions: 312509 Difficulty: Medium
	Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.

	A region is captured by flipping all 'O's into 'X's in that surrounded region.

	For example,
	X X X X
	X O O X
	X X O X
	X O X X
	After running your function, the board should be:

	X X X X
	X X X X
	X X X X
	X O X X

####BFS思路 O(m*n)
- BFS DFS都可以,找到点,看是不是最外层会不被X包住 (检查x = 0, y = 0, x = m -1, y = n -1即可)
- 用了一个arraylist来记录遍历的点,发现被包住,就把他们这些点置为'X',如果不被包住,就不管,所以这里用了一个boolean flag

```java
public class Solution {
    /**
     * @param board a 2D board containing 'X' and 'O'
     * @return void
     */
    private class Node {
        private int x;
        private int y;
        Node(int x, int y) {
            this.x = x;
            this.y = y;
        }

    }

    public void solve(char[][] board) {
        // Write your code here
        if (board.length == 0 || board[0].length == 0) {
            return;
        }

        int m = board.length;
        int n = board[0].length;
        int[][] visited = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (visited[i][j] == 1) {
                    continue;
                }
                visited[i][j] = 1;
                if (board[i][j] != 'O') {
                    continue;
                }
                int[] x = new int[]{0,  1, 0 , -1};
                int[] y = new int[]{1,  0, -1, 0};
                Queue<Node> queue = new LinkedList<Node>();
                List<Node> list = new ArrayList<Node>();
                Node cur = new Node(i,j);
                queue.offer(cur);
                list.add(cur);
                boolean reachLimit = false;

                while (!queue.isEmpty()) {
                    cur = queue.poll();
                    if (cur.x == 0 || cur.y == 0 || cur.x == m - 1 || cur.y == n - 1) {
                        reachLimit = true;
                    }
                    for (int k = 0; k < 4; k++) {
                        int newX = cur.x + x[k];
                        int newY = cur.y + y[k];
                        if (newX >= 0 && newX <= m - 1 && newY >= 0 && newY <= n - 1 && board[newX][newY] == 'O' && visited[newX][newY] == 0) {
                            queue.offer(new Node(newX, newY));
                            list.add(new Node(newX, newY));
                            visited[newX][newY] = 1;
                            if (newX == 0 || newX == m - 1 || newY == 0 || newY == n - 1) {
                                reachLimit = true;
                            }
                        }
                    }
                }

                if (!reachLimit) {
                    for (Node node : list) {
                        board[node.x][node.y] = 'X';
                    }
                }
            }
        }
    }
}
```

####思路2
- Union Find
