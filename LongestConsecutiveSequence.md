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
    /**
     * @param nums: A list of integers
     * @return an integer
     */
    public int longestConsecutive(int[] num) {
        // write you code here
        if (num == null || num.length == 0) {
            return -1;
        }
        int length = num.length;
        Hashtable<Integer,Integer> hashtable = new Hashtable<Integer,Integer>();
        for (int i = 0; i < length; i++) {
            hashtable.put(num[i], i);
        }
        int max = 1;
        int i = 0;
        while (!hashtable.isEmpty() && i < length) {
            int cur;
            int count = 1;
            if (hashtable.containsKey(num[i])) {
                cur = num[i];
                hashtable.remove(cur);
            } else {
                i++;
                continue;
            }
            cur = cur + 1;
            while (hashtable.containsKey(cur)) {
                count++;
                hashtable.remove(cur);
                cur = cur+1;

            }
            cur = num[i] - 1;
            while (hashtable.containsKey(cur)) {
                count++;
                hashtable.remove(cur);
                cur = cur - 1;
            }
            max = Math.max(max, count);
            i++;
        }
        return max;
    }
}

```
