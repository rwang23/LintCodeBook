##Patching Array

	Total Accepted: 7734 Total Submissions: 26829 Difficulty: Medium
	Given a sorted positive integer array nums and an integer n, add/patch elements to the array such that any number in range [1, n] inclusive can be formed by the sum of some elements in the array. Return the minimum number of patches required.

	Example 1:
	nums = [1, 3], n = 6
	Return 1.

	Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
	Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
	Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
	So we only need 1 patch.

	Example 2:
	nums = [1, 5, 10], n = 20
	Return 2.
	The two patches can be [2, 4].

	Example 3:
	nums = [1, 2, 2], n = 5
	Return 0.

####思路
- 用set来存当前sum,每加入一个新的数字,就跟原来set里边数字相加,然后结果保存到list,等set遍历完相加完,就把list的结果加入set, 时间O(n2), 当n特别大的时候超时了
- 需要构造一个贪心的方法

```java
public class Solution {
    public int minPatches(int[] nums, int n) {
        if (nums == null) {
            return -1;
        }

        Set<Integer> sum = new HashSet<Integer>();
        int size = nums.length;

        for (int i = 0; i < size; i++) {
            List<Integer> sumList = new ArrayList<Integer>();
            sumList.add(nums[i]);
            for (Integer s : sum) {
                sumList.add(s + nums[i]);
            }
            for (Integer l : sumList) {
                if (!sum.contains(l)) {
                    sum.add(l);
                }
            }
        }

        int count = 0;
        for (int i = 1; i <= n; i++) {
            List<Integer> sumList = new ArrayList<Integer>();
            if (!sum.contains(i)) {
                sumList.add(i);
                for (Integer s: sum) {
                    sumList.add(s + i);
                }
                count++;
            }
            for (Integer l : sumList) {
                if (!sum.contains(l)) {
                    sum.add(l);
                }
            }
        }
        return count;
    }
}
```

####贪心优化
- [参考](https://leetcode.com/discuss/82822/solution-explanation)

```
Example: Let's say the input is nums = [1, 2, 4, 13, 43] and n = 100. We need to ensure that all sums in the range [1,100] are possible.

Using the given numbers 1, 2 and 4, we can already build all sums from 0 to 7, i.e., the range [0,8). But we can't build the sum 8, and the next given number (13) is too large. So we insert 8 into the array. Then we can build all sums in [0,16).

Do we need to insert 16 into the array? No! We can already build the sum 3, and adding the given 13 gives us sum 16. We can also add the 13 to the other sums, extending our range to [0,29).

And so on. The given 43 is too large to help with sum 29, so we must insert 29 into our array. This extends our range to [0,58). But then the 43 becomes useful and expands our range to [0,101). At which point we're done.


```

```java
public class Solution {
    public int minPatches(int[] nums, int n) {
        long miss = 1;
        int added = 0;
        int i = 0;
        while (miss <= n) {
            if (i < nums.length && nums[i] <= miss) {
                miss += nums[i++];
            } else {
                miss += miss;
                added++;
            }
        }
        return added;
    }
}
```
