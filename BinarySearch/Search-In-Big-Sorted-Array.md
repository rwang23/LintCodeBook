##Search in a Big Sorted Array

39% Accepted

	Given a big sorted array, find the first index of a target number.
    Your algorithm should be in O(log k), where k is the first index of the target number.

	Return -1, if the number doesn't exist in the array.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 3, 6, 9, 21], and target = 3, return 1.

	Given [1, 3, 6, 9, 21], and target = 4, return -1.

####Challenge
O(log k), k is the first index of the given target number.

####Tags Expand
- Binary Search
- Sorted Array

####思路
- 要求O(logk) 那么就去想如何才能logK,只有对原数进行倍增的办法
- 剩下的也就是二分搜索



```java
public class Solution {
    /**
     * @param A: An integer array
     * @param target: An integer
     * @return : An integer which is the index of the target number
     */
    public int searchBigSortedArray(int[] A, int target) {
        // write your code here
        if(A == null || A.length == 0){
            return -1;
        }

        int start = 0;
        int end = A.length - 1;
        while (A[start] < target) {
            start = start*2 + 1;
            if(start > A.length - 1){
                start = end;
                break;
            }
        }
        if (A[start] > target
            start = (start - 1) / 2;
        }

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] == target) {
                end = mid;
            }else if (A[mid] > target) {
                end = mid;
            }else{
                start = mid;
            }
        }

        if (A[start] == target) {
            return start;
        } else if(A[end] == target) {
            return end;
        } else{
            return -1;
        }

    }
}

```
