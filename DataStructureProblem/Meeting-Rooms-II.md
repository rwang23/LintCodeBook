##Meeting Rooms II

	Total Accepted: 8774 Total Submissions: 25814 Difficulty: Medium
	Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

	For example,
	Given [[0, 30],[5, 10],[15, 20]],
	return 2.


####思路
- 解法使用了scan line
- O(nlogn)

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
    public int minMeetingRooms(Interval[] intervals) {
        int size = intervals.length;
        if (size == 0) {
            return 0;
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

        int room = 0;
        int max = 0;
        for (int i = 0; i < 2 * size; i++) {
            if (all[i].status == 0) {
                room++;
                max = Math.max(max, room);
            } else if (all[i].status == 1) {
                room--;
            }

        }

        return max;

    }
}
```
