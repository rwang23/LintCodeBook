##N-Queens II

39% Accepted

	Follow up for N-Queens problem.

	Now, instead outputting board configurations, return the total number of distinct solutions.

	Have you met this question in a real interview? Yes
	Example
	For n=4, there are 2 distinct solutions.

####Tags Expand
- Recursion

####思路
- 跟N-Queen I一样，就是输出结果的size
- 我直接复制战列N-Queen 去掉了draw function
- 再做的可以优化，因为并不需要记录结果，所以不需要result这个arraylist，直接使用一个sum，每次合格，就sum++就行了

```java
public class Solution {
    /**
     * @param n: The number of queens.
     * @return: The total number of distinct solutions.
     */
     
    class Position {
        int x;
        int y;
        Position(int x, int y) {
            this.x = x;
            this.y = y;
        }
    } 
     
    public int totalNQueens(int n) {
        // write your code here
        if (n <= 0) {
            return 0;
        }
        
        List<List<Position>> results = new ArrayList<List<Position>>();
        List<Position> list = new ArrayList<Position>();
        dfs(results, list, n, 0);
        
        return results.size();
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
    
}
```
