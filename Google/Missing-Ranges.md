##Missing Ranges

	Total Accepted: 9886 Total Submissions: 33922 Difficulty: Medium
	Given a sorted integer array where the range of elements are [lower, upper] inclusive, return its missing ranges.

	For example, given [0, 1, 3, 50, 75], lower = 0 and upper = 99, return ["2", "4->49", "51->74", "76->99"].

####思路
- 硬做
- 先判断lower -> nums[0]
- 再判断nums数组里边的
- 再判断nums[size - 1] -> upper
- 同时要注意,如果数组为空,并不是返回为空
- 这个时候返回的是lower -> upper(如果lower和upper一样,就返回一个字符)
- 虽然很简单,但是太容易犯错了

```java
/*

*/

public class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
            List<String> result = new ArrayList<String>();
            if (nums == null) {
                return result;
            }
            if (nums.length == 0) {
                StringBuilder sb = new StringBuilder();
                if (lower == upper) {
                    sb.append(lower);
                } else {
                    sb.append(lower);
                    sb.append("->");
                    sb.append(upper);
                }
                result.add(sb.toString());
                return result;
            }

            int size = nums.length;

            if (lower < nums[0]) {
                StringBuilder sb = new StringBuilder();
                if (lower < nums[0] - 1) {
                    sb.append(lower);
                    sb.append("->");
                    sb.append(nums[0] - 1);
                }  else {
                    sb.append(lower);
                }
                result.add(sb.toString());

            }

            for (int i = 1; i < size; i++) {
                if (nums[i] - nums[i - 1] != 1) {
                    StringBuilder sb = new StringBuilder();
                    if (nums[i] - nums[i - 1] == 2) {
                        sb.append(nums[i - 1] + 1);
                    } else {
                        sb.append(nums[i - 1] + 1);
                        sb.append("->");
                        sb.append(nums[i] - 1);
                    }
                    result.add(sb.toString());
                }
            }

            if (nums[size - 1] < upper) {
                StringBuilder sb = new StringBuilder();
                if (nums[size - 1] < upper - 1) {
                    sb.append(nums[size - 1] + 1);
                    sb.append("->");
                    sb.append(upper);
                } else {
                    sb.append(upper);
                }
                result.add(sb.toString());
            }
            return result;
    }
}
```

####更简洁的写法
- 首先是函数复用
- 其次这个把lower当做了数组第一个数,upper当做了最后一个数

```java
public class Solution {
    public List<String> findMissingRanges(int[] nums, int lower, int upper) {
        List<String> result = new ArrayList<>();
        for (int i = 0; i <= nums.length; i++) {
            int start = i == 0 ? lower : nums[i - 1] + 1;
            int end = i == nums.length ? upper : nums[i] - 1;
            addMissing(result, start, end);
        }
        return result;
    }

    public void addMissing(List<String> result, int start, int end) {
        if (start > end) return;
        else if (start == end) result.add(start + "");
        else result.add(start + "->" + end);
    }
}
```
