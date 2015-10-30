##Remove Element

32% Accepted

	Given an array and a value, remove all occurrences of that value in place and return the new length.

	The order of elements can be changed, and the elements after the new length don't matter.

	Have you met this question in a real interview? Yes
	Example
	Given an array [0,4,4,0,0,2,4,4], value=4

	return 4 and front four elements of the array is [0,0,0,2]

####Tags Expand
- Two Pointers Array

####思路
- 很简单的一道题，但是自己debug了很久 就是因为下标不清
- 以后自己使用两个指针的模板
- 所有都用 start <= end


```java
public class Solution {
    /**
     *@param A: A list of integers
     *@param elem: An integer
     *@return: The new length after remove
     */
    public int removeElement(int[] A, int elem) {
        // write your code here
        if (A == null || A.length == 0) {
            return 0;
        }
        int start = 0;
        int end = A.length - 1;
        while (start <= end) {
            while (start <= end && A[start] != elem) {
                start++;
            }
            while (start <= end && A[end] == elem) {
                end--;
            }
            if (start <= end) {
                exch(A, start, end);
                start++;
                end--;
            }
        }
        return start;
    }
    public void exch(int[] A, int start, int end) {
        int temp = A[start];
        A[start] = A[end];
        A[end] = temp;
    }
}


```
