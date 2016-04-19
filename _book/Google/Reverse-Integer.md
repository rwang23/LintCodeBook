##Reverse Integer

	Total Accepted: 125296 Total Submissions: 531450 Difficulty: Easy
	Reverse digits of an integer.

	Example1: x = 123, return 321
	Example2: x = -123, return -321

	click to show spoilers.

	Have you thought about this?
	Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

	If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

	Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

	For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

####思路
- 用long来处理了overflow

```java
public class Solution {
    public int reverse(int x) {
        return x >= 0 ? reverseNum(x) : -reverseNum(-x);
    }

    public int reverseNum(int x) {
        long sum = 0;
        while (x >= 1) {
            sum *= 10;
            int a = x % 10;
            x /= 10;
            sum += a;
        }

        return sum > Integer.MAX_VALUE ? 0 : (int) sum;
    }
}
```
