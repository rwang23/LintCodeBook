##A + B Problem

51% Accepted

	Write a function that add two numbers A and B. You should not use + or any arithmetic operators.

	Have you met this question in a real interview? Yes
	Example
	Given a=1 and b=2 return 3

	Note
	There is no need to read data from standard input stream. Both parameters are given in function aplusb, you job is to calculate the sum and return it.

	Challenge
	Of course you can just return a + b to get accepted. But Can you challenge not do it like that?

	Clarification
	Are a and b both 32-bit integers?

	Yes.
	Can I use bit operation?

	Sure you can.

####Tags Expand
- Cracking The Coding Interview
- Bit Manipulation

####思路
- 异或就是想加（没有carry的相加）
- 和就是得到进位（相等为0），然后左移，每次去加进位

####例子

	我们来做个3位数的加法：
	101+011=1000 //正常加法
	位运算加法：
	（1） 101 ^ 011 = 110
	(101 & 011)<<1 = 010
	（2） 110 ^ 010 = 100
	(110 & 010)<<1 = 100
	（3） 100 ^ 100 = 000
	(100 & 100)<<1 = 1000
	此时进行相加操作就没有进位了，即000 ^ 1000=1000即是最后结果。

```java
class Solution {
    /*
     * param a: The first integer
     * param b: The second integer
     * return: The sum of a and b
     */

    public int aplusb(int a, int b) {
        if (b == 0) {
            return a;
        }
        int sum = a ^ b;
        int carry = (a & b) << 1;
        return aplusb(sum, carry);
    }

};

```
