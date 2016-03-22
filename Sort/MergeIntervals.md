##Merge Intervals

19% Accepted

	Given a collection of intervals, merge all overlapping intervals.

	Have you met this question in a real interview? Yes
	Example
	Given intervals => merged intervals:

	[                     [
	  [1, 3],               [1, 6],
	  [2, 6],      =>       [8, 10],
	  [8, 10],              [15, 18]
	  [15, 18]            ]
	]

####Challenge
- O(n log n) time and O(1) extra space.

####Tags Expand
- Sort
- Array

####思路
- 需要掌握comparator 也是简化解题的关键

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
    public List<Interval> merge(List<Interval> intervals) {

        if (intervals == null || intervals.size() == 0) {
            return new ArrayList<Interval>();
        }

        Collections.sort(intervals, new Comparator<Interval>(){
            public int compare(Interval i1, Interval i2) {
                if (i1.start != i2.start) {
                    return i1.start - i2.start;
                } else {
                    return i2.end - i2.end;
                }
            }
        });

        int i = 1;
        while (i < intervals.size()) {
            Interval first = intervals.get(i - 1);
            Interval second = intervals.get(i);
            if (first.end >= second.start) {
                first.end = Math.max(first.end, second.end);
                intervals.remove(i);
            } else {
                i++;
            }
        }

        return intervals;
    }
}

```
