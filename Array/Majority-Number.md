##Majority Number

	Given an array of integers,
	the majority number is the number that occurs more than half of the size of the array. Find it.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 1, 1, 1, 2, 2, 2], return 1

####Challenge
O(n) time and O(1) extra space

####Tags Expand
Greedy Enumeration LintCode Copyright Zenefits


####思路
- 来自于一篇论文
- 消除法
- 先找到,然后测试,看到底是不是,因为可能出现并没有majoritynumber的情况
- 当然 也可以排序, 找中间的值,也能实现

```java
public class Solution {
    /**
     * @param nums: a list of integers
     * @return: find a  majority number
     */
    public int majorityNumber(ArrayList<Integer> nums) {
        // write your code
        int size = nums.size();
        int count = 1;
        int candidate = nums.get(0);

        for (int i = 1; i < size; i++) {
            if (candidate == nums.get(i)) {
                count++;
            } else {
                count--;
            }

            if (count == 0) {
                candidate = nums.get(i);
                count = 1;
            }
        }

        count = 0;
        for (int i = 0; i < size; i++) {
            if (nums.get(i) == candidate) {
                count++;
            }
        }

        return count > size / 2 ? candidate : -1;

    }
}
```
