##Majority Number II

	Given an array of integers,
	the majority number is the number that occurs more than 1/3 of the size of the array.

	Find it.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 2, 1, 2, 1, 3, 3], return 1.

	Note
	There is only one majority number in the array.

####Challenge
O(n) time and O(1) extra space.

####Tags Expand
Greedy Enumeration LintCode Copyright Zenefits


####思路
- 其实就是majority number的稍微变形
- 之前是两两相消,这次变成了三三相消
- 我们对count1,count减数时，相当于丢弃了candidate1 candidate2 和当前的数字 一共3个数字
- 但是由于Majority number超过了1/3所以它最后一定会留下来
- 最后还必须检验,到底是candidate1 还是 candidate2, 而且不一定有majority number

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: The majority number that occurs more than 1/3
     */
    public int majorityNumber(ArrayList<Integer> nums) {
        // write your code
        if (nums == null) {
            return -1;
        }
        int size = nums.size();
        int candidate1 = Integer.MIN_VALUE;
        int candidate2 = Integer.MAX_VALUE;
        int count1 = 0;
        int count2 = 0;
        for (int i = 0; i < size; i++) {
            if (nums.get(i) == candidate1) {
                count1++;
            } else if (nums.get(i) == candidate2) {
                count2++;
            } else if (count1 == 0) {
                candidate1 = nums.get(i);
                count1 = 1;
            } else if (count2 == 0) {
                candidate2 = nums.get(i);
                count2 = 1;
            } else if (nums.get(i) != candidate1 && nums.get(i) != candidate2) {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;
        for (int i = 0; i < size; i++) {
            if (nums.get(i) == candidate1) {
                count1++;
            }
            if (nums.get(i) == candidate2) {
                count2++;
            }
        }
        int count = count2 > count1 ? count2 : count1;
        int candidate = (count == count2 ? candidate2 : candidate1);

        return count > size / 3 ? candidate : -1;
    }

}

```
