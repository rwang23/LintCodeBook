##Word Search
	Total Accepted: 69313 Total Submissions: 307323 Difficulty: Medium
	Given a 2D board and a word, find if the word exists in the grid.

	The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

	For example,
	Given board =

	[
	  ['A','B','C','E'],
	  ['S','F','C','S'],
	  ['A','D','E','E']
	]
	word = "ABCCED", -> returns true,
	word = "SEE", -> returns true,
	word = "ABCB", -> returns false.

####思路
- DFS
- 用char比用string要快一些

```java
public class Solution {

    public boolean exist(char[][] board, String word) {
        int m = board.length;
        if (m == 0) {
            throw new IllegalArgumentException("The input is not valid");
        }
        int n = board[0].length;
        if (n == 0) {
            throw new IllegalArgumentException("The input is not valid");
        }
        if (word == null || word.length() == 0) {
            throw new IllegalArgumentException("The input is not valid");
        }

        char[] array = word.toCharArray();
        int[][] isVisited = new int[m][n];

        for (int i = 0; i < m; i++) {
            for (int j= 0; j < n; j++) {
                if (dfs(board, array, isVisited, i, j, 0))
                    return true;
            }
        }

        return false;
    }

    public boolean dfs(char[][] board, char[] array, int[][] isVisited, int x, int y, int index) {

        if (index == array.length - 1 && array[index] == board[x][y]) {
            return true;
        }

        int[] xstep = new int[]{1, -1,  0, 0};
        int[] ystep = new int[]{0,  0, -1, 1};
        boolean isValid = false;

        if (board[x][y] == array[index]) {
            for (int i = 0; i < 4; i++) {
                int newX = x + xstep[i];
                int newY = y + ystep[i];

                if (newX < board.length && newY < board[0].length && newX >= 0 && newY >= 0 && isVisited[newX][newY] == 0) {
                    isVisited[x][y] = 1;
                    isValid = isValid || dfs(board, array, isVisited, newX, newY, index + 1);
                    isVisited[x][y] = 0;
                }
            }
        } else {
            return false;
        }
        return isValid;
    }
}
```
