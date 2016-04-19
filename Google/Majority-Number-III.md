##Majority Number III

	Given an array of integers and a number k,
	the majority number is the number that occurs more than 1/k of the size of the array.

	Find it.

	Have you met this question in a real interview? Yes
	Example
	Given [3,1,2,3,2,3,3,4,4,4] and k=3, return 3.

	Note
	There is only one majority number in the array.

####Challenge
O(n) time and O(k) extra space

####Tags Expand
LintCode Copyright Hash Table Linked List


####思路
- 这个题跟前俩也很像
- 无非就是k低效
- 第一种方法,把majority number ii 写成k层循环的形式,但是这样时间复杂度是O(kn)
- 第二种方法,直接用hashmap去存

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @param k: As described
     * @return: The majority number
     */
    public int majorityNumber(ArrayList<Integer> nums, int k) {
        // count at most k keys.
        HashMap<Integer, Integer> counters = new HashMap<Integer, Integer>();
        for (Integer i : nums) {
            if (!counters.containsKey(i)) {
                counters.put(i, 1);
            } else {
                counters.put(i, counters.get(i) + 1);
            }

            if (counters.size() >= k) {
                removeKey(counters);
            }
        }

        // corner case
        if (counters.size() == 0) {
            return Integer.MIN_VALUE;
        }

        // recalculate counters
        // reset the filtered counters to test
        for (Integer i : counters.keySet()) {
            counters.put(i, 0);
        }
        for (Integer i : nums) {
            if (counters.containsKey(i)) {
                counters.put(i, counters.get(i) + 1);
            }
        }

        // find the max key
        int maxCounter = 0, maxKey = 0;
        for (Integer i : counters.keySet()) {
            if (counters.get(i) > maxCounter) {
                maxCounter = counters.get(i);
                maxKey = i;
            }
        }

        return maxKey;
    }

    private void removeKey(HashMap<Integer, Integer> counters) {
        Set<Integer> keySet = counters.keySet();
        List<Integer> removeList = new ArrayList<>();
        for (Integer key : keySet) {
            counters.put(key, counters.get(key) - 1);
            if (counters.get(key) == 0) {
                removeList.add(key);
            }
        }
        for (Integer key : removeList) {
            counters.remove(key);
        }
    }
}
```
