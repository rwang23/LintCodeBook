##Contains Duplicate
	Total Accepted: 86411 Total Submissions: 209615 Difficulty: Easy
	Given an array of integers, find if the array contains any duplicates.
    Your function should return true if any value appears at least twice in the array,
    and it should return false if every element is distinct.

####思路
- hashmap

```java
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        int size = nums.length;

        if (size == 0) {
            return false;
        }

        Set<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < size; i++) {
            if (set.contains(nums[i])) {
                return true;
            } else {
                set.add(nums[i]);
            }
        }
        return false;
    }
}
```
