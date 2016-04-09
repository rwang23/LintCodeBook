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

####Binary Search
[参考](http://blog.csdn.net/ironyoung/article/details/49664087)

```
如果要修改到 O(n log n) time complexity？贪心法 + 二分搜索。

增加一条辅助的顺序（ordered）栈（队列……完成任务就好），保存尽可能长的LIS。入栈的要求为：

将a[0]入栈
每次取栈顶元素top（最大元素）和读到的元素a[i](0<i<n)做比较：
- 如果a[i] > top 则将a[i]入栈；
- 如果a[i] <= top则二分查找栈中的比a[i]大的第1个数，并用a[i]替换它（如果栈顶元素被替换，说明有机会到达更长序列）；
最长序列长度即为栈的大小
直观理解：对于 x 和 y，如果 x < y 且 stack[y] < stack[x]，用 stack[x] 替换 stack[y]，此时的最长序列长度没有改变，但序列继续变长的''潜力''增大，这就是贪心的目标。

举例：原序列为1，5，8，3，6，7

开始1，5，8相继入栈，此时读到3，用3替换5，得到1，3，8；再读6，用6替换8，得到1，3，6；再读7，得到最终栈为1，3，6，7。最长递增子序列为长度4

但是这个方法，有一个很大的缺陷：只能保证序列长度的正确性，不能保证栈中就是正确的序列。

举例：原序列为1，5，8，2，栈内最后是 1，2，8 不是正确的序列。

分析一下，我们可以看出，虽然有些时候这样得不到正确的序列，但最后算出来的个数是没错的，为什么呢？
```

```java

public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        ArrayList<Integer> lis = new ArrayList<Integer>();
        for (int n : nums) {
            if (lis.size() == 0 || lis.get(lis.size() - 1) < n) {
                lis.add(n);
            } else {
                updateLIS(lis, n);
            }
        }
        return lis.size();
    }

    private void updateLIS(ArrayList<Integer> lis, int n) {
        int l = 0, r = lis.size() - 1;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (lis.get(m) < n) {
                l = m + 1;
            } else {
                r = m;
            }
        }
        lis.set(l, n);
    }
}
```
