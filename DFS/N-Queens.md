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
