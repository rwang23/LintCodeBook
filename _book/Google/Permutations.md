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
- 见注释

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

		//把[]开头的所有排列加入到result里边
		subsetshelper(result, list, nums);
		return result;
	}
	//把list开头的所有排列加入到result里边
	public void subsetshelper(ArrayList<ArrayList<Integer>> result,
	                          ArrayList<Integer> list,
	                          int[] nums) {
		if(list.size()==nums.length){
			result.add(new ArrayList<Integer>(list));
		}

		//把[1]开头的，[2]开头的,[3]开头的，分别加入到result
		for (int i = 0; i < nums.length; i++) {


			if(list.contains(nums[i])){
				continue;
			}
			//把1加入到[]，变成了[1]
			list.add(nums[i]);

			subsetshelper(result, list, nums);
			//试玩[1]开头的。要开始试[2]开头的，就要把[1]取出来
			list.remove(list.size() - 1);
		}
	}
}
```
