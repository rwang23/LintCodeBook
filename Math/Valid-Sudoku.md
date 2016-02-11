##Valid Sudoku

	Determine whether a Sudoku is valid.

	The Sudoku board could be partially filled, where empty cells are filled with the character ..

	Have you met this question in a real interview? Yes
	Example
	The following partially filed sudoku is valid.

	Valid Sudoku

	Note
	A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

	Clarification
	What is Sudoku?

	http://sudoku.com.au/TheRules.aspx
	https://zh.wikipedia.org/wiki/%E6%95%B8%E7%8D%A8
	https://en.wikipedia.org/wiki/Sudoku
	http://baike.baidu.com/subview/961/10842669.htm
####Tags Expand
Matrix Uber


####思路
- [原题有图](http://www.lintcode.com/en/problem/valid-sudoku/)
- 行列,以及九宫格判断
- 难点是九宫格
- 九宫格之前写了四层循环,结果最后有一点出错
- 现在先把每个九宫格当做矩阵
- 然后通过每个九宫格去找index



```java
class Solution {

    public boolean isValidSudoku(char[][] board) {
        if (board.length == 0 || board.length != board[0].length || board.length % 3 != 0) {
            return false;
        }

        int size = board.length;

        for (int i = 0; i < size; i++) {
            HashSet<Character> set = new HashSet<Character>();
            for (int j = 0; j < size; j++) {
                char cur = board[i][j];
                if (set.contains(cur)) {
                    return false;
                }
                if (cur != '.') {
                    set.add(cur);
                }
            }
        }

        for (int i = 0; i < size; i++) {
            HashSet<Character> set = new HashSet<Character>();
            for (int j = 0; j < size; j++) {
                char cur = board[j][i];
                if (set.contains(cur)) {
                    return false;
                }
                if (cur != '.') {
                    set.add(cur);
                }
            }
        }

        int num = size / 3;
        for (int sudoku = 0; sudoku < size * size / 9; sudoku++) {
            int xstart = sudoku / num;
            int ystart = sudoku % num;
            int istart = xstart * 3;
            int jstart = ystart * 3;
            HashSet<Character> set = new HashSet<Character>();
            for (int i = istart; i < istart + 3; i++) {
                for (int j = jstart; j < jstart + 3; j++) {
                    char cur = board[j][i];
                    if (set.contains(cur)) {
                        return false;
                    }
                    if (cur != '.') {
                        set.add(cur);
                    }
                }
            }
        }

        return true;

    }
};
```
