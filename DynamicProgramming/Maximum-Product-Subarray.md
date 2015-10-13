##Maximum Product Subarray

28% Accepted

	Find the contiguous subarray within an array (containing at least one number) which has the largest product.

	Have you met this question in a real interview? Yes
	Example
	For example, given the array [2,3,-2,4], the contiguous subarray [2,3] has the largest product = 6.

##Tags Expand
- Dynamic Programming
- Subarray

####思路
- 实在不行就弄两个变量
- 一大一小
- Maximum Subarray那题的变种。由于正负得负，负负得正的关系。以A[i]结尾的max product subarray同时取决于以A[i-1]结尾的max / min product subarray以及A[i]本身。因此，对每个i，需要记录min/max product两个状态：

```java
public class Solution {
    /**
     * @param nums: an array of integers
     * @return: an integer
     */
    public int maxProduct(int[] A) {
        // write your code here
        if(A == null || A.length == 0){
            return 0;
        }

        int maxLocal = A[0];
        int minLocal = A[0];
        int global = A[0];

        for (int i = 1; i < A.length; i++) {
            int temp = maxLocal;
            maxLocal = Math.max(Math.max(A[i] * maxLocal, A[i]), A[i] * minLocal);
            minLocal = Math.min(Math.min(A[i] * temp, A[i]), A[i] * minLocal);
            global = Math.max(global, maxLocal);
        }
        return global;
    }
}

```
