##N-Queens

20% Accepted

	The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

	Given an integer n, return all distinct solutions to the n-queens puzzle.

	Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.'
	both indicate a queen and an empty space respectively.


	There exist two distinct solutions to the 4-queens puzzle:

	[

	    [".Q..", // Solution 1

	     "...Q",

	     "Q...",

	     "..Q."],

	    ["..Q.", // Solution 2

	     "Q...",

	     "...Q",

	     ".Q.."]

	]

####Challenge
Can you do it without recursion?

####Tags Expand
- Recursion

####思路
- 需要两个funcion,一个是dfs来递归，一个是draw来画图
- 因为要来递归，所以先用ArrayList<Integer>的形式来找满足的图
- 然后在找到所有结果之后再来调用draw，将`ArrayList<Integer>`转化为`ArrayList<String>`
- 关键点去找满足条件的点。画图得知
- 其中string的处理使用了StringBuffer类，这样String处理速度会更快，然后用Str.toString()又转化回了String

####图解释
	0,0 0,1 0,2 0,3
	1,0 1,1 1,2 1,3
	2,0 2,1 2,2 2,3
	3,0 3,1 3,2 3,3

	满足y2 - y1 == Math.abs(x2 -x1) 的位置，两个皇后是会互相攻击的，
	所以两个循环，找到这样的点

####Lintcode
```java
class Solution {
    /**
     * Get all distinct N-Queen solutions
     * @param n: The number of queens
     * @return: All distinct solutions
     * For example, A string '...Q' shows a queen on forth position
     */
    public ArrayList<ArrayList<String>> solveNQueens(int n) {
        // write your code here
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> combo = new ArrayList<Integer>();
        dfs(result, combo, n);
        return draw(result, n);
    }
    public ArrayList<ArrayList<String>> draw(ArrayList<ArrayList<Integer>> source, int n) {
           ArrayList<ArrayList<String>> result = new ArrayList<ArrayList<String>>();
           for (int i = 0; i < source.size(); i++) {
               ArrayList<String> oneline = new ArrayList<String>();
               for (int j = 0; j < n; j++) {
                   int num = source.get(i).get(j);
                   StringBuffer string1 = new StringBuffer("");
                   for (int k = 0; k < n; k++) {
                       if (k != num) {
                           string1.append(".");
                       } else {
                           string1.append("Q");
                       }
                   }
                   String string2 = string1.toString();
                   oneline.add(string2);
               }
               result.add(oneline);
           }

           return result;
    }

    public void dfs(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> combo, int n) {
        // for (int i = 0; i < combo.size(); i++) {
        //     int x1 = combo.get(i);
        //     for(int j = i + 1; j < combo.size(); j++) {
        //         int x2 = combo.get(j);
        //         if (j - i == Math.abs(x2 -x1)) {
        //             return;
        //         }
        //     }
        // }
        if (!isValid(combo)) {
            return;
        }

        if (combo.size() == n) {
            result.add(new ArrayList<Integer>(combo));
            return;
        }
        for (int i = 0; i < n; i++) {
            if (combo.contains(i)){
               continue;
            }
            combo.add(i);
            dfs(result, combo, n);
            combo.remove(combo.size() - 1);
        }
    }

    public boolean isValid(ArrayList<Integer> list) {
        if (list == null || list.size() == 0) {
            return true;
        }
        int y1 = list.size() - 1;
        int x1 = list.get(y1);
        for (int i = 0; i < list.size() - 1; i++) {
            int y2 = i;
            int x2 = list.get(y2);
            if (Math.abs(y2 - y1) == Math.abs(x2 - x1)) {
                return false;
            }
        }

        return true;
    }
};


```

####Leetcode
```java
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        if (n <= 0) {
            return new ArrayList<List<String>>();
        }
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> queens = new ArrayList<Integer>();
        Set<Integer> set = new HashSet<Integer>();
        dfs(result, queens, set, n);
        List<List<String>> board = printBoard(result, n);

        return board;
    }

    public void dfs(List<List<Integer>> result, List<Integer> queens, Set<Integer> set, int n) {
        if (!isValid(queens)) {
            return;
        }
        if (queens.size() == n) {
            result.add(new ArrayList<Integer>(queens));
            return;
        }

        for (int i = 0; i < n; i++) {
            if (!set.contains(i)) {
                queens.add(i);
                set.add(i);
                dfs(result, queens, set, n);
                set.remove(i);
                queens.remove(queens.size() - 1);
            }
        }
    }

    public boolean isValid(List<Integer> queens) {
        if (queens == null || queens.size() == 0) {
            return true;
        }
        int size = queens.size();
        int curX = size - 1;
        int curY = queens.get(curX);
        for (int i = 0; i < size - 1; i++) {
            int x = i;
            int y = queens.get(x);
            if (curX - x == Math.abs(curY - y)) {
                return false;
            }
        }
        return true;
    }

    public List<List<String>> printBoard(List<List<Integer>> input, int n) {
        List<List<String>> result = new ArrayList<List<String>>();
        if (input == null || input.size() == 0) {
            return result;
        }
        for (int i = 0; i < input.size(); i++) {
            List<Integer> curBoard = input.get(i);
            List<String> oneBoard = new ArrayList<String>();
            for (int j = 0; j < curBoard.size(); j++) {
                StringBuilder string = new StringBuilder();
                for (int k = 0; k < n; k++) {
                    if (curBoard.get(j) != k) {
                        string.append('.');
                    }
                    else {
                        string.append('Q');
                    }
                }
                oneBoard.add(string.toString());
            }
            result.add(oneBoard);
        }
        return result;
    }
}
```
