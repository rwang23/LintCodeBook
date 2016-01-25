## Subsets II

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
- 在subsets I的基础上添加限制条件
- 当[1,2,2]后，回到[1,2]后，不再出现[1,2,2]；当有[2],[2,2]后不再出现[2],[2,2] 所以这一位跟上一位不能一样 并且同时：
- 但是[1,2,2]与[2,2]是可以出现的，只有顺序输出的12有用，也就是pos==i时
- i = pos的时候， 比如1，2 第三个数 pos=i=2，所以要输出[1,2,2]
- 只有顺序输出的12有用，

```java
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public ArrayList<ArrayList<Integer>> subsetsWithDup(ArrayList<Integer> S) {
		// write your code here
		ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
		ArrayList<Integer> list = new ArrayList<Integer>() ;
		int[] nums = new int[S.size()];
		for (int i = 0; i < nums.length; i++) {
			nums[i] = S.get(i).intValue();
		}
		Arrays.sort(nums);

		int pos = 0;
		subsetshelper(result, list, nums, pos);
		return result;
	}

	public void subsetshelper(ArrayList<ArrayList<Integer>> result,
	                          ArrayList<Integer> list,
	                          int[] nums,
	                          int pos) {
		result.add(new ArrayList<Integer>(list));
		for (int i = pos; i < nums.length; i++) {
			if (i != pos && nums[i] == nums[i - 1]) {
				continue;
			}
			list.add(nums[i]);
			subsetshelper(result, list, nums, i + 1);
			list.remove(list.size() - 1);
		}
	}
}
```

####另一种思考方式
- 不在递归循环中去进行判断，而是在结果中进行判断
- 如果该结果已经出现过了，就不再加入了（一定是122 以第一个2为基础的时候先出现）

```java
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public ArrayList<ArrayList<Integer>> subsetsWithDup(ArrayList<Integer> S) {
		// write your code here
		ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
		ArrayList<Integer> list = new ArrayList<Integer>() ;
		int[] nums = new int[S.size()];
		for (int i = 0; i < nums.length; i++) {
			nums[i] = S.get(i).intValue();
		}
		Arrays.sort(nums);

		int pos = 0;
		subsetshelper(result, list, nums, pos);
		return result;
	}

	public void subsetshelper(ArrayList<ArrayList<Integer>> result,
	                          ArrayList<Integer> list,
	                          int[] nums,
	                          int pos) {
	    if(!result.contains(list)) {
		    result.add(new ArrayList<Integer>(list));
	    }
		for (int i = pos; i < nums.length; i++) {
// 			if (i != pos && nums[i] == nums[i - 1]) {
// 				continue;
// 			}
			list.add(nums[i]);
			subsetshelper(result, list, nums, i + 1);
			list.remove(list.size() - 1);
		}
	}
}
```

