##Meeting Rooms
	Total Accepted: 8006 Total Submissions: 19442 Difficulty: Easy
	Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

	For example,
	Given [[0, 30],[5, 10],[15, 20]],
	return false.

####思路
- 自己用了scan line的数据结构
- O(nlogn)
- 其实直接做更简单,见下面

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

    public class segment {
        int val;
        int status;
        segment(int val, int status) {
            this.val = val;
            this.status = status;
        }
    }
    public boolean canAttendMeetings(Interval[] intervals) {
        int size = intervals.length;
        if (size <= 1) {
            return true;
        }

        segment[] all = new segment[size * 2];
        for (int i = 0; i < size; i++) {
            segment start = new segment(intervals[i].start, 0);
            segment end = new segment(intervals[i].end, 1);
            all[2 * i] = start;
            all[2 * i + 1] = end;
        }

        Arrays.sort(all, new Comparator<segment>(){
            public int compare(segment s1, segment s2) {
                if (s1.val != s2.val) {
                    return s1.val - s2.val;}
                else {
                    return s2.status - s1.status;
                }
            }
        });

        for (int i = 0; i + 1 < 2 * size; i++) {
            if (all[i].status == all[i + 1].status) {
                return false;
            }
        }

        return true;

    }
}
```

####直接做
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

    public boolean canAttendMeetings(Interval[] intervals) {
      if (intervals == null)
        return false;

      // Sort the intervals by start time
      Arrays.sort(intervals, new Comparator<Interval>() {
        public int compare(Interval a, Interval b) { return a.start - b.start; }
      });

      for (int i = 1; i < intervals.length; i++)
        if (intervals[i].start < intervals[i - 1].end)
          return false;

      return true;
    }
}
```
