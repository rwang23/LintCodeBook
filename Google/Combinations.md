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
		List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> combo = new ArrayList<Integer>();
        dfs(result, combo, 1, n, k);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> combo, int pos, int n, int k) {
        if (combo.size() == k) {
            result.add( new ArrayList<Integer>(combo));
        } else if (combo.size() > k || pos > n) {
            return;
        }

        for (int i = pos; i <= n; i++) {
            combo.add(i);
            dfs(result, combo, i + 1, n, k);
            combo.remove(combo.size() - 1);
        }
    }
}

```
