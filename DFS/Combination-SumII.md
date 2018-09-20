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

####进一步优化
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
            result.add(new ArrayList<Integer>(list));
            return;
        }
        if (target < 0) {
            return;
        }

        for (int i = position; i < candidates.length; i++) {
	    /*
	    此处需要思考，只有当与前者元素相等，且进入下一层的情况，那么才将相同重复的元素添加
	    否则只会创建一个相同的list
	    [1,1,2,4,5,7]
	    第一次拿了1 然后找到了比如1,2,4
	    如果没有去重的话，在第二1的时候，又会创建一个1,2,4的list（此时还在循环里，两个1都在递归同层）
	    只有当我们需要多个1的时候，需要取1,1,5这样的list的时候，我们才会继续添加1进去（此时第一个1在递归的下上层）
	    所有只有i == postion &&  candidates[i] == candidates[i - 1]时，我们继续，否则只能continue
	    */
            if (i > position && candidates[i] == candidates[i - 1]) {
                continue;
            }
            list.add(candidates[i]);
            dfs(result, list, candidates, target - candidates[i], i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```
