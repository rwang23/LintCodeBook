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

###非递归思路1
- [参考](https://www.letiantian.me/2014-11-29-permutation-combination-non-recursive-algorithms/)
- 全排列就是从第一个数字起每个数分别与它后面的数字交换
- 去重的全排列就是从第一个数字起每个数分别与它后面非重复出现的数字交换
- 全排列的非递归就是由后向前找替换数和替换点，然后由后向前找第一个比替换数大的数与替换数交换，最后颠倒替换点后的所有数据。


###非递归思路2
- [参考](https://blog.csdn.net/happyaaaaaaaaaaa/article/details/51534048)
- 假设我们有了当前前 i 个元素的组合，当第 i+1个元素加入时，我们需要做的是将这个元素加入之前的每一个结果，并且放在每个结果的每个位置，因为之前的结果没有重复，所以加入新元素的结果也不会有重复（这里是假定数字集合没有重复）


```javapublic class Solution {
     public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> first = new ArrayList<>();
        first.add(nums[0]);
        res.add(first);
        for(int i = 1; i < nums.length; i++) {
            List<List<Integer>> newRes = new ArrayList<>();
            for(List<Integer> temp : res) {
                int size = temp.size() + 1;
                for(int j = 0; j < size; j++) {
                    List<Integer> item = new ArrayList<>(temp);
                    item.add(j, nums[i]);
                    newRes.add(item);
                }
            }
            res = newRes;
        }
        return res;
    }
}
```
