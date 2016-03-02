##String to Integer (atoi)
	Total Accepted: 90150 Total Submissions: 674994 Difficulty: Easy
	Implement atoi to convert a string to an integer.

	Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

	Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

	Update (2015-02-10):
	The signature of the C++ function had been updated. If you still see your function signature accepts a const char * argument, please click the reload button  to reset your code definition.

	spoilers alert... click to show requirements for atoi.

	Requirements for atoi:
	The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

	The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

	If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

	If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

####思路
- test case各种限制条件
- 根据test case写了六次, 惭愧
- 找个时间再做一次

```java
public class Solution {
    public int myAtoi(String str) {
        if (str == null) {
            //throw new NullPointerException("null input");
            return 0;
        }

        long sum = 0;
        int isPositive = 1;
        boolean alreadySign = false;
        boolean alreadyNum = false;

        for (int i = 0; i < str.length(); i++) {
            char c = str.charAt(i);

            if (c == ' ' && !alreadyNum) {
                continue;
            }
            if (c == ' ' && alreadyNum) {
                return (int)sum;
            }

            if (c == ('-')) {
                if (alreadySign) {
                    return 0;
                } else {
                    isPositive = -1;
                    alreadySign = true;
                }
                alreadyNum = true;
                continue;
            }

            if (c == ('+')) {
                if (alreadySign) {
                    return 0;
                } else {
                    alreadySign = true;
                }
                alreadyNum = true;
                continue;
            }

            if ((c < '0' || c > '9')) {
                //throw new IllegalArgumentException("invalid input");
                sum = isPositive * sum;
                sum = (sum > Integer.MAX_VALUE) ? Integer.MAX_VALUE : sum;
                sum = (sum < Integer.MIN_VALUE) ? Integer.MIN_VALUE : sum;
                return (int) sum;
            }
            sum *= 10;
            int cur = c - '0';
            sum += cur;
            alreadyNum = true;
            if (sum > Integer.MAX_VALUE) {
                sum = isPositive * sum;
                sum = (sum > Integer.MAX_VALUE) ? Integer.MAX_VALUE : sum;
                sum = (sum < Integer.MIN_VALUE) ? Integer.MIN_VALUE : sum;
                return (int)sum;
            }
        }

        sum = isPositive * sum;
        sum = (sum > Integer.MAX_VALUE) ? Integer.MAX_VALUE : sum;
        sum = (sum < Integer.MIN_VALUE) ? Integer.MIN_VALUE : sum;

        return (int)sum;

    }
}
```
