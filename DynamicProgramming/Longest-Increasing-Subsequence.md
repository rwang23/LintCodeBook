##Longest Increasing Subsequence

26% Accepted

	Given a sequence of integers, find the longest increasing subsequence (LIS).

	You code should return the length of the LIS.

	Have you met this question in a real interview? Yes
	Example
	For [5, 4, 1, 2, 3], the LIS  is [1, 2, 3], return 3

	For [4, 2, 4, 5, 3, 7], the LIS is [4, 4, 5, 7], return 4

####Challenge
- Time complexity O(n^2) or O(nlogn)

####Clarification
What's the definition of longest increasing subsequence?

    * The longest increasing subsequence problem is to find a subsequence of a given sequence
    in which the subsequence's elements are in sorted order, lowest to highest,
    and in which the subsequence is as long as possible.
    This subsequence is not necessarily contiguous, or unique.

    * https://en.wikipedia.org/wiki/Longest_common_subsequence_problem

####Tags Expand
- Binary Search
- LintCode Copyright
- Dynamic Programming

####思路
- 一定要好好把过程想明白，画一遍
- 不一定是return aux[n] 而是max
- 这个题以后要多自己再想想
- 见注释

```java
public class Solution {
    /**
     * @param nums: The integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        // write your code here

	    // /**
        //  * state: aux[i] 表示前i个数字中，以第i 个数结尾的aux中，有多少个LLS
        //  * function: aux[i] = max{aux[i],aux[j]+1  j<i && nums[j] <= nums[i] }
        //  *          如果当前 aux［i］的值大于 aux[j]+1 的值， 则不变，否则
        //  *          aux[i] = aux[j]+1
        //  * initialize: aux[0,,,n]=1
        //  *              因为每个元素 最短序列起码可以是它自己。容易出错误的点是：
        //  *              初始化的时候只把 lis[0]付值为1
        //  * answer：max（aux[0,,,n]）
        //  */
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int[] aux = new int[nums.length];
        aux[0] = 1;
        int max = 0;
        for (int i = 1; i < nums.length; i++) {
            aux[i] = 1;
            for (int j = 0; j < i; j++) {
                if (nums[i] >= nums[j]) {
                    aux[i] = Math.max(aux[i], aux[j] + 1);
                }
            }
            max = Math.max(max,aux[i]);
        }
        return max;

    }
}

```
