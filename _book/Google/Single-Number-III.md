##Single Number III

	Given 2*n + 2 numbers, every numbers occurs twice except two, find them.

	Have you met this question in a real interview? Yes
	Example
	Given [1,2,2,3,4,4,5,3] return 1 and 5

####Challenge
O(n) time, O(1) extra space.

####Tags Expand
Greedy LintCode Copyright


####思路
- [参考](http://bookshadow.com/weblog/2015/08/17/leetcode-single-number-iii/)
- 分成两拨
- 首先计算nums数组中所有数字的异或，记为xor
- 令lowbit = xor & -xor，lowbit的含义为xor从低位向高位，第一个非0位所对应的数字
- 例如假设xor = 6（二进制：0110），则-xor为（二进制：1010，-6的补码，two's complement）
- 则lowbit = 2（二进制：0010）
- 根据异或运算的性质，“同0异1”
- 记只出现一次的两个数字分别为a与b
- 可知a & lowbit与b & lowbit的结果一定不同
- 通过这种方式，即可将a与b拆分开来

```java
public class Solution {
    /**
     * @param A : An integer array
     * @return : Two integers
     */
    public List<Integer> singleNumberIII(int[] nums) {
        // write your code here
        if (nums == null || nums.length < 1) {
            return new ArrayList<Integer>();
        }

        int distinctBit = 0;
        List<Integer> result = new ArrayList<Integer>();
        for (int i = 0; i < nums.length; i++) {
            distinctBit ^= nums[i];
        }

        distinctBit = distinctBit & (-distinctBit);

        int first = 0, second = 0;
        for (int i = 0; i < nums.length; i++) {
            if ((nums[i] & distinctBit) == 0) {
                first ^= nums[i];
            } else {
                second ^= nums[i];
            }
        }

        result.add(first);
        result.add(second);
        return result;
    }
}

```
