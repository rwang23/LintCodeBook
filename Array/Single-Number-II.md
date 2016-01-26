##Single Number II

Given 3*n + 1 numbers, every numbers occurs triple times except one, find it.

Have you met this question in a real interview? Yes
Example
Given [1,1,2,3,3,3,2,2,4,1] return 4

####Challenge
One-pass, constant extra space.

####Tags Expand
Greedy

####解法
- 主要考察的就是 异或 运算
- 一般我们使用异或是 两个数 等的位 就为0, 不等的位就1
- 其实就是不进位的加法
- 正常二进制异或的时候 假设 0和1,最后得到1,其实就是加起来%2, 0 0 0 0 和 1 1,最后就是0
- 这里我们尝试将每一位加起来 %3
- 再还原出这个数


```java
public class Solution {
	/**
	 * @param A : An integer array
	 * @return : An integer
	 */
    public int singleNumberII(int[] A) {
        // write your code here
        if (A == null || A.length == 0) {
            return -1;
        }
        int size = A.length;
        int result = 0;
        int[] bits = new int[32];
        for (int i = 0; i < 32; i++) {
            for (int j = 0; j < size; j++) {
                bits[i] += (A[j] >> i) & 1;
                bits[i] %= 3;
            }
            result = result | (bits[i] << i);
        }

        return result;
    }
}

```
