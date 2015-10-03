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

####思路
- 三个数取一次
- 就算先取了2，也必须回过去找1，所以可以用不设限制条件的循环，重新去找1
- 如果又遇到了2，跳过就可以




```java
class Solution {
    /**
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> S) {
		// write your code here
		ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
		ArrayList<Integer> list = new ArrayList<Integer>() ;
		if(S==null || S.size()==0){
			return result;
		}
		int[] nums = new int[S.size()];

		for (int i = 0; i < nums.length; i++) {
			nums[i] = S.get(i).intValue();
		}
		Arrays.sort(nums);


		subsetshelper(result, list, nums);
		return result;
	}

	public void subsetshelper(ArrayList<ArrayList<Integer>> result,
	                          ArrayList<Integer> list,
	                          int[] nums) {
		if(list.size()==nums.length){
			result.add(new ArrayList<Integer>(list));
		}


		for (int i = 0; i < nums.length; i++) {


			if(list.contains(nums[i])){
				continue;
			}

			list.add(nums[i]);

			subsetshelper(result, list, nums);

			list.remove(list.size() - 1);
		}
	}
}
```
