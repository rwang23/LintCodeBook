##Permutations

	Given a list of numbers, return all possible permutations.

	For nums = [1,2,3], the permutations are:

	[
	  [1,2,3],
	  [1,3,2],
	  [2,1,3],
	  [2,3,1],
	  [3,1,2],
	  [3,2,1]
	]

####Challenge
- Do it without recursion.

####Tags: Recursion

####递归思路
- 三个数取一次
- 就算先取了2，也必须回过去找1，所以可以用不设限制条件的循环，重新去找1
- 如果又遇到了2，跳过就可以


```java
public class Solution {
    /*
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public List<List<Integer>> permute(int[] nums) {
        // write your code here
        List<List<Integer>> results = new ArrayList<List<Integer>>();
        
        if (nums == null || nums.length == 0) {
            results.add(new ArrayList<Integer>());
            return results;
        }
        
        boolean[] visited = new boolean[nums.length];
        List<Integer> list = new ArrayList<Integer>();
        
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
            
            list.add(nums[i]);
            visited[i] = true;
            dfs(results, list, nums, visited);
            visited[i] = false;
            list.remove(list.size() - 1);
        }
    }
}
```

###非递归思路
- [参考](https://www.letiantian.me/2014-11-29-permutation-combination-non-recursive-algorithms/)
