##Sudoku Solver

	Total Accepted: 48400 Total Submissions: 195551 Difficulty: Hard
	Write a program to solve a Sudoku puzzle by filling the empty cells.

	Empty cells are indicated by the character '.'.

	You may assume that there will be only one unique solution.

####思路
- 跟N-Queen问题很像
- DFS
- isValid就是valid sudoku那道题的做法

```java
public class Solution {
    public void solveSudoku(char[][] board) {
        dfs(board);
    }

    public boolean dfs(char[][] board) {
        for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++){
                if(board[i][j] != '.'){
                    continue;
                }
                for(int k = 1; k <= 9; k++){
                    board[i][j] = (char) (k + '0');
                    if (isValid(board, i, j) && dfs(board)){
                        return true;
                    }
                    board[i][j] = '.';
                }
                return false;
            }
        }
        return true;
    }

    private boolean isValid(char[][] board, int i, int j) {

        for (int k = 0; k < 9; k++) {
            if(k != j && board[i][k] == board[i][j]) {
                return false;
            }
        }
        for (int k = 0; k < 9; k++) {
            if(k != i && board[k][j] == board[i][j]) {
                return false;
            }
        }
        for (int row = i / 3 * 3; row< i / 3 * 3 + 3; row++) {
            for (int col = j / 3 * 3; col < j / 3 * 3 + 3; col++) {
                if ((row != i || col != j) && board[row][col] == board[i][j]) {
                    return false;
                }
            }
        }
        return true;
    }
}
```
