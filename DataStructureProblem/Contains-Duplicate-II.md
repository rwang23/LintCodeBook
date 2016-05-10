##Contains Duplicate II
	Total Accepted: 55906 Total Submissions: 186871 Difficulty: Easy
	Given an array of integers and an integer k,
    find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j]
    and the difference between i and j is at most k.

####思路
- idea1:两层for loop, O(kn)
- idea2:设置一个类或者hashmap记录下index,然后sort,然后找 O(nlogn)
- idea3:直接hashmap,存在对应的List里边,再找

```java
public class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k <= 0) {
            return false;
        }

        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
        int size = nums.length;
        for (int i = 0; i < size; i++) {
            if (map.containsKey(nums[i])) {
                map.get(nums[i]).add(i);
            } else {
                List<Integer> list = new ArrayList<Integer>();
                list.add(i);
                map.put(nums[i], list);
            }
        }

        for (Map.Entry<Integer, List<Integer>> entry : map.entrySet()) {
            List<Integer> list = entry.getValue();
            Collections.sort(list);
            for (int i = 0; i < list.size() - 1; i++) {
                int first = list.get(i);
                int second = list.get(i + 1);
                if (second - first <= k) {
                    return true;
                }
            }
        }

        return false;
    }
}
```
