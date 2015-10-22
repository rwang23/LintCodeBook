##Find Peak Element

45% Accepted


    There is an integer array which has the following features:

	The numbers in adjacent positions are different.
	A[0] < A[1] && A[A.length - 2] > A[A.length - 1].
	We define a position P is a peek if:

	A[P] > A[P-1] && A[P] > A[P+1]
	Find a peak element in this array. Return the index of the peak.

	Have you met this question in a real interview? Yes
	Example
	Given [1, 2, 1, 3, 4, 5, 7, 6]

	Return index 1 (which is number 2) or 6 (which is number 7)

####Note
The array may contains multiple peeks, find any of them.

####Challenge
Time complexity O(logN)

####Tags Expand
- Binary Search
- Array

####思路
- 划分成小问题
- 二分搜索
- 注意边界


####优化前
- 可能有边界问题
- start + 1 start - 1 end + 1 end - 1都有可能出现问题

```java
class Solution {
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        // write your code here
        if(A == null || A.length <= 2 ){
            return -1;
        }

        int start = 0;
        int end = A.length -1;

        while(start + 1 < end){
            int mid = start + (end - start) / 2;
            if( (A[mid] > A[mid-1]) && (A[mid] > A[mid+1]) ){
                return mid;
            }else if(A[mid] < A[mid+1]){
                start = mid;
            }else if(A[mid] > A[mid+1]){
                end = mid;
            }
        }

        if( (A[start] > A[start + 1]) && (A[start] > A[start - 1]) ){
            return start;
        }else if( (A[end] > A[end + 1]) && (A[end] > A[end - 1]) ){
            return end;
        }else{
            return -1;
        }
    }
}
```

####优化后
- 没有了边界问题

```java
class Solution {
    /**
     * @param A: An integers array.
     * @return: return any of peek positions.
     */
    public int findPeak(int[] A) {
        // write your code here
        int start = 1, end = A.length-2; // 1.答案在之间，2.不会出界
        while(start + 1 <  end) {
            int mid = (start + end) / 2;
            if(A[mid] < A[mid - 1]) {
                end = mid;
            } else if(A[mid] < A[mid + 1]) {
                start = mid;
            } else {
                end = mid;
            }
        }
        if(A[start] < A[end]) {
            return end;
        } else {
            return start;
        }
    }
}
```
