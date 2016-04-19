##Combination Sum III

	Total Accepted: 28816 Total Submissions: 81692 Difficulty: Medium
	Find all possible combinations of k numbers that add up to a number n,
	given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

	Ensure that numbers within the set are sorted in ascending order.


	Example 1:

	Input: k = 3, n = 7

	Output:

	[[1,2,4]]

	Example 2:

	Input: k = 3, n = 9

	Output:

	[[1,2,6], [1,3,5], [2,3,4]]

####思路

```java
public class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> combo = new ArrayList<Integer>();
        dfs(result, combo, k, n, 1);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> combo, int k, int n, int position) {
        if (k == 0 && n == 0) {
            result.add(new ArrayList<Integer>(combo));
            return;
        }

        if (k < 0 || n < 0) {
            return;
        }

        for (int i = position; i <= 9; i++) {
            combo.add(i);
            dfs(result, combo, k - 1, n - i, i + 1);
            combo.remove(combo.size() - 1);
        }
    }

}
```
