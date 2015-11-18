##Total Occurrence of Target

17% Accepted

	Given a target number and an integer array sorted in ascending order.
	Find the total number of occurrences of target in the array.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 3, 3, 4, 5] and target = 3, return 2.

	Given [2, 2, 3, 4, 6] and target = 4, return 1.

	Given [1, 2, 3, 4, 5] and target = 6, return 0.

####Challenge
Time complexity in O(logn)

####Tags Expand
Binary Search

####思路
- search for range变形,找左边界,再找右边界,index相减加1即可

```java
public class Solution {
    /**
     * @param A an integer array sorted in ascending order
     * @param target an integer
     * @return an integer
     */
    public int totalOccurrence(int[] A, int target) {
        if (A == null || A.length == 0) {
            return 0;
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
            return 0;
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
            return 0;
        }

        return bound[1] - bound[0] + 1;
    }

}

```
