##Jump Game

39% Accepted

	Given an array of non-negative integers, you are initially positioned at the first index of the array.

	Each element in the array represents your maximum jump length at that position.

	Determine if you are able to reach the last index.

	Have you met this question in a real interview? Yes
	Example
	A = [2,3,1,1,4], return true.

	A = [3,2,1,0,4], return false.

####Note

	This problem have two method which is Greedy and Dynamic Programming.

	The time complexity of Greedy method is O(n).

	The time complexity of Dynamic Programming method is O(n^2).

	We manually set the small data set to allow you pass the test in both ways. This is just to let you learn how to use this problem in dynamic programming ways. If you finish it in dynamic programming ways, you can try greedy method to make it accept again.

####Tags Expand
- Greedy
- Array

####思路
- 一个辅助状态数组 定义为存放 max(f(n-1) - 1, this.val)
- 这样就能判断是否可以跳过去
- O(n), 九章的解法是O(n2)

```java
public class Solution {
    /**
     * @param A: A list of integers
     * @return: The boolean answer
     */
    public boolean canJump(int[] A) {
        // wirte your code here
        if (A.length <= 2) {
            if(A.length >= 1 && A[0] >= 1){
                return true;
            }else {
                return false;
            }
        }

        int[] truth = new int[A.length];
        truth[0] = A[0];
        for (int i = 1; i < A.length - 1; i++) {
            if (truth[i-1]>=1) {
                truth[i] = Math.max(truth[i-1] - 1, A[i]);
            } else {
                truth[i] = 0;
            }
        }

        return truth[A.length - 2] >= 1;
    }
}


```
