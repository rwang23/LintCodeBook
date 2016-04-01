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
class Solution {
    /**
     * Calculate the total number of distinct N-Queen solutions.
     * @param n: The number of queens.
     * @return: The total number of distinct solutions.
     */
    public int totalNQueens(int n) {
        ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
        ArrayList<Integer> combo = new ArrayList<Integer>();
        dfs(result, combo, n);
        return result.size();
    }


    public void dfs(ArrayList<ArrayList<Integer>> result, ArrayList<Integer> combo, int n) {
        for (int i = 0; i < combo.size(); i++) {
            int x1 = combo.get(i);
            for(int j = i + 1; j < combo.size(); j++) {
                int x2 = combo.get(j);
                if (j - i == Math.abs(x2 -x1)) {
                    return;
                }
            }
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
};

```

####优化后
```java
public class Solution {
    public static int sum;
    public int totalNQueens(int n) {
        sum = 0;
        int[] usedColumns = new int[n];
        placeQueen(usedColumns, 0);
        return sum;
    }
    public void placeQueen(int[] usedColumns, int row) {
        int n = usedColumns.length;

        if (row == n) {
            sum ++;
            return;
        }

        for (int i = 0; i < n; i++) {
            if (isValid(usedColumns, row, i)) {
                usedColumns[row] = i;
                placeQueen(usedColumns, row + 1);
            }
        }
    }
    public boolean isValid(int[] usedColumns, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (usedColumns[i] == col) {
                return false;
            }
            if ((row - i) == Math.abs(col-usedColumns[i])) {
                return false;
            }
        }
        return true;
    }
}
```
