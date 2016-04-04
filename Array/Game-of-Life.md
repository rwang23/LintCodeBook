##Game of Life

	Total Accepted: 15633 Total Submissions: 46058 Difficulty: Medium

	According to the Wikipedia's article: "The Game of Life, also known simply as Life,
	is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

	Given a board with m by n cells, each cell has an initial state live (1) or dead (0).
	Each cell interacts with its eight neighbors (horizontal, vertical, diagonal)
	using the following four rules (taken from the above Wikipedia article):

	Any live cell with fewer than two live neighbors dies, as if caused by under-population.
	Any live cell with two or three live neighbors lives on to the next generation.
	Any live cell with more than three live neighbors dies, as if by over-population..
	Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
	Write a function to compute the next state (after one update) of the board given its current state.

	Follow up:
	Could you solve it in-place?
	Remember that the board needs to be updated at the same time:
	You cannot update some cells first and then use their updated values to update other cells.
	In this question, we represent the board using a 2D array.
	In principle, the board is infinite,
	which would cause problems when the active area encroaches the border of the array.
	How would you address these problems?

####思路
- 把input当做储存
- 找周围是否有Live点,并且把board[i][j]周围的live点个数储存在board[i][j]
- 如果这个点本身是dead的,那么就储存负值
- 有一个容易错的地方就是,如果这个点本身是Live的,但是周围没有live点,所以countLive == 0,这个时候不能把这个0储存进这个点,否则遍历到下一个点的时候就会忽略掉此点
- 再来一轮遍历,如果该点值满足规则,就置为live否则就是dead

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) {
            return;
        }

        int m = board.length;
        int n = board[0].length;
        int[] xstep = new int[]{-1, -1, -1, 0, 0, 1, 1, 1};
        int[] ystep = new int[]{-1, 0, 1, -1, 1, -1, 0, 1};

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int countLive = 0;
                for (int k = 0; k < 8; k++) {
                    int newX = i + xstep[k];
                    int newY = j + ystep[k];
                    if (newX >= 0 && newY >= 0 && newX < m && newY < n) {
                        if (board[newX][newY] >= 1) {
                            countLive++;
                        }
                    }
                }
                if (board[i][j] == 1) {
                    if (countLive != 0) {
                        board[i][j] = countLive;
                    }
                } else {
                    board[i][j] = 0 - countLive;
                }

            }
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int life = board[i][j];
                if (life >= 0) {
                    if (life == 2 || life == 3) {
                        board[i][j] = 1;
                    } else {
                        board[i][j] = 0;
                    }
                } else {
                    if (life == -3) {
                        board[i][j] = 1;
                    } else {
                        board[i][j] = 0;
                    }
                }
            }
        }
    }
}
```
