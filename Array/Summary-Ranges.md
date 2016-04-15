##Summary Ranges

	Total Accepted: 43843 Total Submissions: 182282 Difficulty: Medium
	Given a sorted integer array without duplicates, return the summary of its ranges.

	For example, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

####思路
- 硬做题

```java
public class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> result = new ArrayList<String>();
        if (nums == null || nums.length == 0) {
            return result;
        }

        int size = nums.length;
        if (size == 1) {
            String s = Integer.toString(nums[0]);
            result.add(s);
            return result;
        }

        int start = nums[0];
        int end = nums[0];
        int range = 1;
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i < size; i++) {
            if (nums[i] != nums[i - 1] + 1) {
                if (start == end) {
                    sb.append(start);
                } else {
                    sb.append(start);
                    sb.append("->");
                    sb.append(end);
                }
                result.add(new String(sb.toString()));
                start = nums[i];
                end = nums[i];
                sb = new StringBuilder();
            } else {
                end = nums[i];
            }
            if (i == size - 1) {
                if (start == end) {
                    sb.append(start);
                } else {
                    sb.append(start);
                    sb.append("->");
                    sb.append(end);
                }
                result.add(new String(sb.toString()));
            }
        }
        return result;
    }
}
```
