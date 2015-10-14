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
- 我自己用的quick sort 然而并不需要
- Java有自己的库 Collection.sort
- 需要掌握comparator
- 九章的解法 spaca单独用了一个arraylist, 自己的解法就在原地进行，只使用了一个 int len

####修改后的解法
```java
public class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() <= 1) {
            return intervals;
        }

        Collections.sort(intervals, new IntervalComparator());

        int len = intervals.size();
        for (int i = 1; i < len; ) {
            if (intervals.get(i).start <= intervals.get(i - 1).end) {
                intervals.get(i - 1).end = Math.max(intervals.get(i - 1).end,intervals.get(i).end) ;
                intervals.remove(i);
                len--;

            } else {
                i++;
            }
        }
        return intervals;
    }


    private class IntervalComparator implements Comparator<Interval> {
        public int compare(Interval a, Interval b) {
            return a.start - b.start;
        }
    }

}
```

----
####我的代码
```java
/**
 * Definition of Interval:
 * public class Interval {
 *     int start, end;
 *     Interval(int start, int end) {
 *         this.start = start;
 *         this.end = end;
 *     }
 */

class Solution {
    /**
     * @param intervals: Sorted interval list.
     * @return: A new sorted interval list.
     */
    public List<Interval> merge(List<Interval> intervals) {
        // write your code here

        int len = intervals.size();
        sort(intervals, 0, len - 1);
        for (int i = 1; i < len; ) {
            if (intervals.get(i).start <= intervals.get(i - 1).end) {
                intervals.get(i - 1).end = Math.max(intervals.get(i - 1).end,intervals.get(i).end) ;
                intervals.remove(i);
                len--;

            } else {
                i++;
            }
        }
        return intervals;
    }

    public void sort(List<Interval> intervals, int lo, int hi) {
        if (hi <= lo) {
            return;
        }
        int j = partition(intervals, lo, hi);
        sort(intervals, lo, j - 1);
        sort(intervals, j + 1 , hi);
    }

    public int partition(List<Interval> intervals, int lo, int hi) {
        int i = lo;
        int j = hi + 1;
        while (true) {
            while (intervals.get(++i).start < intervals.get(lo).start) {
                if (i == hi) {
                    break;
                }
            }
            while (intervals.get(--j).start > intervals.get(lo).start) {
                if (j == lo) {
                    break;
                }
            }
            if (i >= j) {
                break;
            }
            exchange(intervals, i, j);
        }
        exchange(intervals, lo, j);
        return j;
    }

    public void exchange(List<Interval> intervals, int index1, int index2) {
        Interval temp = new Interval(0,0);
        temp.start = intervals.get(index1).start;
        temp.end = intervals.get(index1).end;

        intervals.get(index1).start = intervals.get(index2).start;
        intervals.get(index1).end = intervals.get(index2).end;

        intervals.get(index2).start = temp.start;
        intervals.get(index2).end = temp.end;

    }
}

```
