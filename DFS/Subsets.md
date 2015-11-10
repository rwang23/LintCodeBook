
##Subsets I

	Given a set of distinct integers, return all possible subsets.

	If S = [1,2,3], a solution is:
	[
	  [3],
	  [1],
	  [2],
	  [1,2,3],
	  [1,3],
	  [2,3],
	  [1,2],
	  []
	]

#### Note

- Elements in a subset must be in non-descending order.

- The solution set must not contain duplicate subsets.

####Tags: Recursion

###思路
- DFS
- 当循环中i=0时，是以1开头的，在循环中pos+1进入递归，所以会有[1,2]和[1,3]，[1,2]再递归得到[1,2,3]。因为[1,3]时i==2，所以无法继续递归
- 当循环中i=1时，是以2开头的，以此类推

```java
class Solution {
	/**
	 * @param S: A set of numbers.
	 * @return: A list of lists. All valid subsets.
	 */
	public ArrayList<ArrayList<Integer>> subsets(ArrayList<Integer> S) {
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
			list.add(nums[i]);
			subsetshelper(result, list, nums, i + 1);
			list.remove(list.size()-1);
		}
	}
}
```


####Non-recursion
- 记忆

