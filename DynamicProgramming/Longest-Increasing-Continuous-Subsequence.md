##Longest Increasing Continuous subsequence

26% Accepted

	Give you an integer array (index from 0 to n-1, where n is the size of this array)，find the longest increasing continuous subsequence in this array. (The definition of the longest increasing continuous subsequence here can be from right to left or from left to right)

	Have you met this question in a real interview? Yes
	Example
	For [5, 4, 2, 1, 3], the LICS is [5, 4, 2, 1], return 4.

	For [5, 1, 2, 3, 4], the LICS is [1, 2, 3, 4], return 4.

####Note
- O(n) time and O(1) extra space.

####Tags Expand
- Dynamic Programming
- Array

####思路
- DP

```java
public class Solution {
    /**
     * @param A an array of Integer
     * @return  an integer
     */
    public int longestIncreasingContinuousSubsequence(int[] A) {
        // Write your code here
        if (A.length < 2) {
            return A.length;
        }
        int ret = 1;
        int max = 0;
        for (int i = 1; i < A.length; i++) {
            if(A[i] > A[i-1]) {
                ret++;
                max = Math.max(ret, max);
            } else {
                ret = 1;
            }
        }
        ret = 1;
        for (int i = 1; i < A.length; i++) {
            if(A[i] < A[i-1]) {
                ret++;
                max = Math.max(ret, max);
            } else {
                ret = 1;
            }
        }
        return max;
    }
}

```
