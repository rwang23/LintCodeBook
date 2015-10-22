##Search for a Range

20% Accepted

	Given a sorted array of n integers,
    find the starting and ending position of a given target value.

	If the target is not found in the array, return [-1, -1].

	Have you met this question in a real interview? Yes
	Example
	Given [5, 7, 7, 8, 8, 10] and target value 8, return [3, 4].

##Challenge
- O(log n) time.

##Tags Expand
- Binary Search
- Sorted Array
- Array

##思路
- 先找前一个再找后一个index
- if (A[mid] == target) {end = mid;} 前面一个的时候 这么赋值 找前面的，找后面的时候相反

```java
public class Solution {
    public int[] searchRange(int[] A, int target) {
        if (A.length == 0) {
            return new int[]{-1, -1};
        }

        int start, end, mid;
        int[] bound = new int[2];

        // search for left bound
        start = 0;
        end = A.length - 1;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (A[mid] == target) {
                end = mid;
            } else if (A[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[start] == target) {
            bound[0] = start;
        } else if (A[end] == target) {
            bound[0] = end;
        } else {
            bound[0] = bound[1] = -1;
            return bound;
        }

        // search for right bound
        start = 0;
        end = A.length - 1;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;
            if (A[mid] == target) {
                start = mid;
            } else if (A[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if (A[end] == target) {
            bound[1] = end;
        } else if (A[start] == target) {
            bound[1] = start;
        } else {
            bound[0] = bound[1] = -1;
            return bound;
        }

        return bound;
    }
}
```
