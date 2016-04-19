##Insert Interval

	Total Accepted: 54811 Total Submissions: 233202 Difficulty: Hard
	Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

	You may assume that the intervals were initially sorted according to their start times.

	Example 1:
	Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].

	Example 2:
	Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].

	This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

####思路 O(n)
- 思路很简单,设置一个result,就是不断比较再加入
- 特别是 允许 start == end ,就是[6,6]这种interval,在原来的结构上现加上判断代码
- 但是好多corner case啊
- 面试的时候一定要问清楚,能不能允许[6, 6],如果不允许,那么久好太多了

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {

        List<Interval> result = new ArrayList<Interval>();
        if (newInterval == null || newInterval.start > newInterval.end) {
            return intervals;
        }

        if (intervals == null || intervals.size() == 0) {
            result.add(newInterval);
            return result;
        }

        if (newInterval.end < intervals.get(0).start) {
            intervals.add(0, newInterval);
            return intervals;
        }

        if (newInterval.start > intervals.get(intervals.size() - 1).end) {
            intervals.add(newInterval);
            return intervals;
        }

        int i = 0;
        for (i = 0; i < intervals.size(); i++) {
            Interval cur = intervals.get(i);
            if (newInterval.end < cur.start) {
                result.add(newInterval);
                break;
            }
            if (newInterval.start <= cur.end) {
                cur.end = Math.max(newInterval.end, cur.end);
                cur.start = Math.min(newInterval.start, cur.start);
                result.add(cur);
                i++;
                break;
            }
            result.add(cur);
        }

        while (i < intervals.size()) {
            Interval cur = result.get(result.size() - 1);
            Interval next = intervals.get(i);

            if (cur.end >= next.start) {
                cur.end = Math.max(cur.end, next.end);
            } else {
                result.add(next);
            }
            i++;
        }

        return result;
    }
}
```

####简化版代码,上面太冗长了
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {

    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {

        List<Interval> result = new ArrayList<Interval>();

        for (Interval i : intervals) {
            if (newInterval == null || i.end < newInterval.start) {
                result.add(i);
            } else if (i.start > newInterval.end) {
                result.add(newInterval);
                result.add(i);
                newInterval = null;
            } else {
                newInterval.start = Math.min(newInterval.start, i.start);
                newInterval.end = Math.max(newInterval.end, i.end);
            }
        }

        if (newInterval != null) {
            result.add(newInterval);
        }

        return result;
    }

}
```
