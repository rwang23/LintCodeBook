##Longest Consecutive Sequence

33% Accepted

	Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

	Have you met this question in a real interview? Yes
	Example
	Given [100, 4, 200, 1, 3, 2],
	The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

####Clarification
Your algorithm should run in O(n) complexity.

####Tags Expand
- Array

####思路
- 因为是O(n)，所以就不能排序等方法，动规去做好像目测也是不能在O(n)实现的
- 所以想到hashmap，用空间换时间
- 花了一点时间debug，因为程序中hashtable.remove(cur) 写反了 cur = cur+1;

```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int len = nums.length;
        Set<Integer> set = new HashSet<Integer>();

        for (int i = 0; i < len; i++) {
            if (!set.contains(nums[i])) {
                set.add(nums[i]);
            }
        }

        int maxLen = 0;
        for (int i = 0; i < len; i++) {
            if (set.contains(nums[i])) {
                int countLen = 1;
                int cur = nums[i];
                set.remove(cur);
                while (set.contains(++cur)) {
                    countLen++;
                    set.remove(cur);
                }
                cur = nums[i];
                while (set.contains(--cur)) {
                    countLen++;
                    set.remove(cur);
                }
                maxLen = Math.max(maxLen, countLen);
            }
        }

        return maxLen;
    }
}
```
