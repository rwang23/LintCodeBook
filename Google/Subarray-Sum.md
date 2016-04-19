##Subarray Sum

25% Accepted

	Given an integer array, find a subarray where the sum of numbers is zero.
	Your code should return the index of the first number and the index of the last number.

	Have you met this question in a real interview? Yes
	Example
	Given [-3, 1, 2, -3, 4], return [0, 2] or [1, 3].

	Note
	There is at least one subarray that it's sum equals to zero.

####思路

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A list of integers includes the index of the first number
     *          and the index of the last number
     */
    public ArrayList<Integer> subarraySum(int[] nums) {
        // write your code here

        int len = nums.length;

        ArrayList<Integer> ans = new ArrayList<Integer>();
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();

        map.put(0, -1);

        int sum = 0;
        for (int i = 0; i < len; i++) {
            sum += nums[i];

            if (map.containsKey(sum)) {
                ans.add(map.get(sum) + 1);
                ans.add(i);
                return ans;
            }

            map.put(sum, i);
        }

        return ans;
    }
}

```
