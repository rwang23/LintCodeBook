##Permutations II

	Given a list of numbers with duplicate number in it. Find all unique permutations.

	For numbers [1,2,2] the unique permutations are:

	[

	    [1,2,2],

	    [2,1,2],

	    [2,2,1]

	]

####Challenge
Do it without recursion.

####Tags: Recursion

####思路
- PermutationI 加上去重，见注释

```
public class Solution {
    /*
     * @param :  A list of integers
     * @return: A list of unique permutations
     */
    public List<List<Integer>> permuteUnique(int[] nums) {
        // write your code hereList<List<Integer>> results = new ArrayList<List<Integer>>();
        List<List<Integer>> results = new ArrayList<List<Integer>>();

        if (nums == null || nums.length == 0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        
        boolean[] visited = new boolean[nums.length];
        List<Integer> list = new ArrayList<Integer>();
        Arrays.sort(nums);
        
        dfs(results, list, nums, visited);
        
        return results;
        
    }
    
    public void dfs(List<List<Integer>> results, List<Integer> list, int[] nums, boolean[] visited) {
        
        if (list.size() == nums.length) {
            List<Integer> target = new ArrayList<Integer>(list);
            results.add(target);
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            //去重，已经有visited，直接利用起来，如果相邻两个数相等，而且上一个没被访问过，那么一定不是从上一层下来的，就是在本层里的循环，这样会导致重复
            if (i >=1 && !visited[i - 1] && nums[i] == nums[i - 1]) {
                continue;
            }
            
            list.add(nums[i]);
            visited[i] = true;
            dfs(results, list, nums, visited);
            visited[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```
