##The Smallest Difference

36% Accepted

	Given two array of integers(the first array is array A, the second array is array B), now we are going to find a element in array A which is A[i], and another element in array B which is B[j], so that the difference between A[i] and B[j] (|A[i] - B[j]|) is as small as possible, return their smallest difference.

	Example
	For example, given array A = [3,6,7,4], B = [2,8,9,3], return 0

####Challenge
O(n log n) time

####Tags Expand
Two Pointers LintCode Copyright Sort Array

####思路
- 两种解法，一种是通过二分，一种是通过two pointers
- 拿到这道题的时候，就想到了先排序再二分查找
- 注意自己写二分的规范，免得边界条件容易出错，比如 end = mid,自己第一次写成了end = mid -1，这纠错了
- two pointers也是很好的方法

####二分
```java
public class Solution {
    /**
     * @param A, B: Two integer arrays.
     * @return: Their smallest difference.
     */
    public int smallestDifference(int[] A, int[] B) {
        // write your code here
        Arrays.sort(A);
        Arrays.sort(B);
        int minDistance = Integer.MAX_VALUE;
        for (int i = 0; i < A.length; i++) {
            int end = B.length - 1;
            int start = 0;

            while (start + 1 < end) {
                int mid = start + (end - start) / 2;
                if (B[mid] > A[i]) {
                    end = mid;
                } else if (B[mid] < A[i]) {
                    start = mid;
                } else {
                    return 0;
                }
            }
            minDistance = Math.min(Math.min(Math.abs(B[start] - A[i]), Math.abs(B[end] - A[i])), minDistance);
        }
        return minDistance;
    }
}
```

####Two Pointers
```java

public class Solution {
    public int smallestDifference(int[] A, int[] B) {
        Arrays.sort(A);
        Arrays.sort(B);

        int i = 0, j = 0;
        int min = Integer.MAX_VALUE;

        while (i < A.length && j < B.length) {
            min = Math.min(min, Math.abs(A[i] - B[j]));
            if (A[i] <= B[j]) {
                i++;
            } else {
                j++;
            }
        }
        return min;
    }
}
```
