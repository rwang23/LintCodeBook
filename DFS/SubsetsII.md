##Subsets II

	Given a list of numbers that may has duplicate numbers, return all possible subsets

	If S = [1,2,2], a solution is:

	[
	  [2],
	  [1],
	  [1,2,2],
	  [2,2],
	  [1,2],
	  []
	]

####Note
	- Each element in a subset must be in non-descending order.

	- The ordering between two subsets is free.

	- The solution set must not contain duplicate subsets.

####Tag
- Recursion


####思路
- 在递归条件中直接进行了判断
- 当[1,2,2]后，回到[1,2]后，不再出现[1,2,2]；当有[2],[2,2]后不再出现[2],[2,2] 所以这一位跟上一位不能一样 并且同时：
- 但是[1,2,2]与[2,2]是可以出现的，只有顺序输出的12有用，也就是pos==i时
- i = pos的时候， 比如1，2 第三个数 pos=i=2，所以要输出[1,2,2]
- 只有顺序输出的12有用，

```java
public class Solution {
    /**
     * @param nums: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        // write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        if (nums == null || nums.length == 0) {
            result.add(list);
            return result;
        }

        Arrays.sort(nums);
        dfs(result, list, nums, 0);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> list, int[] nums, int pos) {

        result.add(new ArrayList<Integer>(list));

        for (int i = pos; i < nums.length; i++) {
	     /*
	    此处需要思考，只有当与前者元素相等，且进入下一层的情况，那么才将相同重复的元素添加
	    否则只会创建一个相同的list
	    [1,1,2,4,5,7]
	    第一次拿了1 然后找到了比如1,2,4
	    如果没有去重的话，在第二1的时候，又会创建一个1,2,4的list（此时还在循环里，两个1都在递归同层）
	    只有当我们需要多个1的时候，需要取1,1,5这样的list的时候，我们才会继续添加1进去（此时第一个1在递归的下上层）
	    所有只有i == postion &&  candidates[i] == candidates[i - 1]时，我们继续，否则只能continue
	    */
            if (i != pos && nums[i] == nums[i - 1]) {
                continue;
            }
            list.add(nums[i]);
            dfs(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}

```



