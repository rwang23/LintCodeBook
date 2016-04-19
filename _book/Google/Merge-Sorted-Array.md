##Merge Sorted Array

	Given two sorted integer arrays A and B, merge B into A as one sorted array.

	Have you met this question in a real interview? Yes
	Example
	A = [1, 2, 3, empty, empty], B = [4, 5]

	After merge, A will be filled as [1, 2, 3, 4, 5]

	Note
	You may assume that A has enough space (size that is greater or equal to m + n) to hold additional elements from B. The number of elements initialized in A and B are m and n respectively.

####Tags Expand
Sorted Array Array Facebook

####思路
- 不断比较最大的,然后放在最后就行

```java
class Solution {
    /**
     * @param A: sorted integer array A which has m elements,
     *           but size of A is m+n
     * @param B: sorted integer array B which has n elements
     * @return: void
     */
    public void mergeSortedArray(int[] A, int m, int[] B, int n) {
        // write your code here

        while (m >= 1 || n >= 1) {
            if (m == 0 && n > 0) {
                A[n - 1] = B[n - 1];
                n--;
            } else if (n == 0 && m > 0) {
                return;
            } else if (A[m - 1] >= B[n - 1]) {
                A[m + n - 1] = A[m - 1];
                m--;
            } else if (A[m - 1] < B[n - 1]) {
                A[m + n - 1] = B[n - 1];
                n--;
            }
        }

    }
}
```
