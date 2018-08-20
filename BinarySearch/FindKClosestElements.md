##Find K Closest Elements
	Given a target number, a non-negative integer k and an integer array A sorted in ascending order,
	find the k closest numbers to target in A,
	sorted in ascending order by the difference between the number and target.
	Otherwise, sorted in ascending order by number if the difference is same.

##Example
	Given A = [1, 2, 3], target = 2 and k = 3, return [2, 1, 3].

	Given A = [1, 4, 6, 8], target = 3 and k = 3, return [4, 1, 6].

##Challenge
	O(logn + k) time complexity.

##Notice
	The value k is a non-negative integer and will always be smaller than the length of the sorted array.
	Length of the given array is positive and will not exceed 10^4
	Absolute value of elements in the array and x will not exceed 10^4


##思路
- 找到最近接的两个,其中一个可以等于target
- 然后两根指针比较,左边的左移,右边的右移,注意index不要越界


```java
public class Solution {
    /**
     * @param A: an integer array
     * @param target: An integer
     * @param k: An integer
     * @return: an integer array
     */
    public int[] kClosestNumbers(int[] A, int target, int k) {
        // write your code here
        int[] result = new int[k];
        if (A.length == 0 || k == 0) {
            return result;
        }

        int start = 0;
        int end = A.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (A[mid] >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        int index = 0;
        while (start >= 0 && end <= A.length - 1 && index < k) {

            if (Math.abs(A[start] - target) <= Math.abs(A[end] - target)) {
                result[index] = A[start];
                start--;
            } else {
                result[index] = A[end];
                end++;
            }

            index++;

            while (start < 0 && index < k) {
                result[index++] = A[end++];
            }

            while (end > A.length - 1 && index < k) {
                result[index++] = A[start--];
            }
        }

        return result;
    }
}
```
