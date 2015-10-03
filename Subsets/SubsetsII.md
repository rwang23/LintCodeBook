## Subsets II

### Given a list of numbers that may has duplicate numbers, return all possible subsets

	If S = [1,2,2], a solution is:

	[
	  [2],
	  [1],
	  [1,2,2],
	  [2,2],
	  [1,2],
	  []
	]

###Note
- Each element in a subset must be in non-descending order.

- The ordering between two subsets is free.

- The solution set must not contain duplicate subsets.

####Tag:Recursion

###思路
- 在subsets I的基础上添加限制条件
-

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
