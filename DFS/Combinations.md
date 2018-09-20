##Combinations

31% Accepted

	Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

	Have you met this question in a real interview? Yes
	Example
	For example,
	If n = 4 and k = 2, a solution is:
	[[2,4],[3,4],[2,3],[1,2],[1,3],[1,4]]

####Tags Expand
- Backtracking Array


```java
public class Solution {
    /**
     * @param n: Given the range of numbers
     * @param k: Given the numbers of combinations
     * @return: All the combinations of k numbers out of 1..n
     */
    public List<List<Integer>> combine(int n, int k) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        List<Integer> combination = new ArrayList<Integer>();
        if (n <= 0 || n < k) {
            results.add(combination);
            return results;
        }
        
        dfs(results, combination, n, k, 1);
        return results;
    }
    
    public void dfs(List<List<Integer>> results, List<Integer> combination, int n, int k, int start) {
        
        if (k == 0) {
            List<Integer> cur = new ArrayList<Integer>(combination);
            results.add(cur);
            return;
        }
        
        for (int i = start; i <= n; i++) {
            
            combination.add(i);
            dfs(results, combination, n, k - 1, i + 1);
            combination.remove(combination.size() - 1);
        }
    }
}
```
