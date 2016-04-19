##Divide Two Integers

	Total Accepted: 64518 Total Submissions: 412438 Difficulty: Medium
	Divide two integers without using multiplication, division and mod operator.

	If it is overflow, return MAX_INT.

####思路
- 下面这种利用减法的超时了

```java
public class Solution {
    public int divide(int dividend, int divisor) {
        if (divisor == 0) {
            return Integer.MAX_VALUE;
        }

        boolean sign1 = false;
        if (divisor < 0) {
            sign1 = true;
            divisor = 0 - divisor;
        }
        boolean sign2 = false;
        if (dividend < 0) {
            sign2 = true;
            dividend = 0 - dividend;
        }
        int result = 0;
        while (dividend >= divisor) {
            dividend -= divisor;
            result++;
        }

        return (sign1 ^ sign2) ? result : 0 - result;
    }
}
```

####倍增优化
- 先<<1找到最大的可能的除数,
- 然后每回合>>1 就是除以2
- 注意corner case,比如输入divident时Integer.MIN_VALUE,divisor是-1,就有可能溢出
- 先都把他们撩为正数,最后求结果的时候(dividend < 0) ^ (divisor < 0) 来判断符号(符号相等结果不变)

```java
public class Solution {
    public int divide(int dividend, int divisor) {

        if (divisor == 0) {
            return Integer.MAX_VALUE;
        }

        long divd = dividend;
        long divs = divisor;
        if (divd < 0) {
            divd = 0 - divd;
        }
        if (divs < 0) {
            divs = 0 - divs;
        }

        long digit = 1;
        while ((divs << 1) <= divd) {
            divs = divs << 1;
            digit = digit << 1;
        }

        long result = 0;
        while (divd > 0 && divs >= divisor) {
            if (divd >= divs) {
                divd -= divs;
                result += digit;
            } else {
                divs = divs >> 1;
                digit = digit >> 1;
            }
        }

        result = (dividend < 0) ^ (divisor < 0) ? -result : result;
        if (result > Integer.MAX_VALUE || result < Integer.MIN_VALUE) {
            return Integer.MAX_VALUE;
        }
        return (int)result;
    }
}
```
