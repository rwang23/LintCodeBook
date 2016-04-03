##Counting Bits

	Total Accepted: 10069 Total Submissions: 18123 Difficulty: Medium
	Given a non negative integer number num.
	For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

	Example:
	For num = 5 you should return [0,1,1,2,1,2].

	Follow up:

	It is very easy to come up with a solution with run time O(n*sizeof(integer)).
	But can you do it in linear time O(n) /possibly in a single pass?
	Space complexity should be O(n).
	Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

####思路
- 暴力解法,每个数都走32遍去看有几个1,面试肯定不行
- [参考](http://articles.leetcode.com/number-of-1-bits/)
- [非常棒的图](http://www.programcreek.com/2015/03/leetcode-counting-bits-java/)
- 使用了第二种思路,也非常好理解

```java
public class Solution {
    public int[] countBits(int num) {
        int[] result = new int[num + 1];
        result[0] = 0;
        int powOfTwo = 0;
        for (int i = 1; i <= num; i++) {
            if ((i & (i - 1)) == 0) {
                result[i] = 1;
                powOfTwo = i;
            } else {
                result[i] = result[powOfTwo] + result[i - powOfTwo];
            }
        }

        return result;
    }
}
```
