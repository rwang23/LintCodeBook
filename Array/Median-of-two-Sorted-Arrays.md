##Median of two Sorted Arrays Show result

21% Accepted

	There are two sorted arrays A and B of size m and n respectively.
    Find the median of the two sorted arrays.

	Have you met this question in a real interview? Yes
	Example
	Given A=[1,2,3,4,5,6] and B=[2,3,4,5], the median is 3.5.

	Given A=[1,2,3] and B=[4,5], the median is 3.

####Challenge
The overall run time complexity should be O(log (m+n)).

####Tags Expand
- Sorted Array
- Divide and Conquer
- Array

####思路
- 该题给的是sorted array,那么O(m+n) 常规解法就能解决问题，但是既然不是m+n，就要想办法优化
- log(m+n)想到使用二分法，所以每次必然要扔掉k/2个数
- 怎么扔呢？比较A第k/2的数与B第k/2的数，谁大说明median number在另一边，所以扔掉另一边的前k/2，而median就在后边
- 这个时候，要找的第k大的数，变成了k/2大
- 分治法递归

```java
class Solution {
    /**
     * @param A: An integer array.
     * @param B: An integer array.
     * @return: a double whose format is *.5 or *.0
     */
    public double findMedianSortedArrays(int[] A, int[] B) {
        // write your code here
        if (A == null && B == null) {
            return Integer.MIN_VALUE;
        }
        if ((A.length + B.length) % 2 == 0) {
            return (findkthnumber(A, 0, B, 0, (A.length + B.length) / 2 + 1) + findkthnumber(A, 0, B, 0, (A.length + B.length) / 2)) / 2.0;
        } else {
            return findkthnumber(A, 0, B, 0, (A.length + B.length) / 2 + 1);
        }
    }

    public int findkthnumber(int[] A, int A_start,
                                int[] B, int B_start,
                                int k) {
        if (A_start >= A.length) {
			return B[B_start + k - 1];
		}
		if (B_start >= B.length) {
			return A[A_start + k - 1];
		}

		if (k == 1) {
			return Math.min(A[A_start], B[B_start]);
		}


        int A_key = A_start + k / 2 - 1 < A.length
		            ? A[A_start + k / 2 - 1 ]
		            : Integer.MAX_VALUE;
		int B_key = B_start + k / 2 - 1 < B.length
		            ? B[B_start + k / 2 - 1]
		            : Integer.MAX_VALUE;

        if (A_key > B_key) {
            return  findkthnumber(A, A_start, B, B_start + k /2, k - k / 2);
        } else {
            return findkthnumber(A, A_start + k / 2, B, B_start, k - k / 2);
        }
    }
}


```
