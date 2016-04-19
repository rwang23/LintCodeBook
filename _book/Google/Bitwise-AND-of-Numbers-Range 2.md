##Bitwise AND of Numbers Range

	Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

	For example, given the range [5, 7], you should return 4.

	Credits:
	Special thanks to @amrsaqr for adding this problem and creating all test cases.

####Tags
Bit Manipulation

####思路
- 画出0 - 15的 bits
- 发现如果从m一直AND到n,那如果某位有0的,最后这个位一定也是0
- 当m与n不相等时,就开始向右移位,直到相等
- 这中间向右移位是因为这些位最后都会为0

```java
public class Solution {
    public int rangeBitwiseAnd(int m, int n) {

        int count = 0;
        while (m != n) {
            m >>= 1;
            n >>= 1;
            count++;
        }

        return m<<=count;
    }

}
```
