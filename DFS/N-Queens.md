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

####解法

```java
public class Solution {
    /*
     * @param n: The number of queens
     * @return: All distinct solutions
     */
    
    class Position {
        int x;
        int y;
        Position(int x, int y) {
            this.x = x;
            this.y = y;
        }
    } 
     
    public List<List<String>> solveNQueens(int n) {
        // write your code here
        List<List<String>> graph = new ArrayList<List<String>>();
        
        if (n <= 0) {
            return graph;
        }
        
        List<List<Position>> results = new ArrayList<List<Position>>();
        List<Position> list = new ArrayList<Position>();
        dfs(results, list, n, 0);
        
        graph = draw(results, n);
        
        return graph;
    }
    
    public void dfs(List<List<Position>> results, List<Position> list, int n, int level) {
        
        if (list.size() == n) {
            results.add(new ArrayList<Position>(list));
            return;
        }
        
        for (int i = 0; i < n; i++) {
            Position cur = new Position(level, i);
            if (!checkRule(list, cur)) {
                continue;
            }
            
            list.add(cur);
            dfs(results, list, n, level + 1);
            list.remove(list.size() - 1);
        }
    }
    
    public boolean checkRule(List<Position> list, Position cur) {
        
        for (Position prev : list) {
            
            if (prev.x == cur.x || prev.y == cur.y) {
                return false;
            }
            if (Math.abs(prev.x - cur.x) == Math.abs(prev.y - cur.y)) {
                return false;
            }
        }
        
        return true;
    }
    
    public List<List<String>> draw(List<List<Position>> results, int n) {
        
        List<List<String>> graph = new ArrayList<List<String>>();
        
        if (results == null || results.size() == 0) {
            return graph;
        }
        
        for (List<Position> positionList : results) {
            List<String> graphList = new ArrayList<String>();
            
            for (Position position : positionList) {
                int y = position.y;
                
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < n; i++) {
                    if (i != y) {
                        sb.append(".");
                    } else {
                        sb.append("Q");
                    }
                }
                graphList.add(sb.toString());
            }
            graph.add(graphList);
        }
        
        return graph;
        
    }
}
```
