##Combination Sum II

26% Accepted

	Given a collection of candidate numbers (C) and a target number (T),
	find all unique combinations in C where the candidate numbers sums to T.

	Each number in C may only be used once in the combination.

	Have you met this question in a real interview? Yes
	Example
	For example, given candidate set 10,1,6,7,2,1,5 and target 8,

	A solution set is:

	[1,7]

	[1,2,5]

	[2,6]

	[1,1,6]

####Note
	All numbers (including target) will be positive integers.
	Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
	The solution set must not contain duplicate combinations.
####Tags Expand
- Backtracking Array
- Combination Sum I变形题，只需要改一下加入条件，以及每次pos = pos + 1

```java
public class Solution {
    /**
     * @param candidates: A list of integers
     * @param target:An integer
     * @return: A list of lists of integers
     */
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        // write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> combo = new ArrayList<Integer>();
        Arrays.sort(candidates);
        dfs(result, combo, candidates, 0, target, 0);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> combo, int[] candidates, int pos, int target, int sum) {

        if (sum > target) {
            return;
        } else if (sum == target && !result.contains(combo)) {
            result.add(new ArrayList<Integer>(combo));
        }

        for (int i = pos; i <candidates.length; i++) {

            combo.add(candidates[i]);
            sum += candidates[i];
            dfs(result, combo, candidates, i+1, target, sum);
            sum -= candidates[i];
            combo.remove(combo.size() - 1);
        }
    }
}
```

####稍微优化
- 在每次进入下一次递归的时候,检查
- 如果i != 0 && candidates[i] == candidates[i - 1] && !list.contains(candidates[i])
- 就不用进入了,这样速度提高了三倍

```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        if (candidates == null || candidates.length == 0) {
            return new ArrayList<List<Integer>>();
        }
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        Arrays.sort(candidates);
        dfs(result, list, candidates, target, 0);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> list, int[] candidates, int target, int position) {
        if (target == 0) {
            if (!result.contains(list)) {
                result.add(new ArrayList<Integer>(list));
            }
            return;
        }
        if (target < 0) {
            return;
        }

        for (int i = position; i < candidates.length; i++) {
            if (i != 0 && candidates[i] == candidates[i - 1] && !list.contains(candidates[i])) {
                continue;
            }
            list.add(candidates[i]);
            dfs(result, list, candidates, target - candidates[i], i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```
