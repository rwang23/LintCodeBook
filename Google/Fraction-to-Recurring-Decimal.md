##Fraction to Recurring Decimal

    Total Accepted: 29360 Total Submissions: 195406 Difficulty: Medium
    Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

    If the fractional part is repeating, enclose the repeating part in parentheses.

    For example,

    Given numerator = 1, denominator = 2, return "0.5".
    Given numerator = 2, denominator = 1, return "2".
    Given numerator = 2, denominator = 3, return "0.(6)".
    Hint:

    No scary math, just apply elementary math knowledge.
    Still remember how to perform a long division?
    Try a long division on 4/9, the repeating part is obvious. Now try 4/333. Do you see a pattern?
    Be wary of edge cases! List out as many test cases as you can think of and test your code thoroughly.

####思路
- 最开始一点思路都没有
- 看了解析才恍然大悟,
- 通过每次*10,来不断求小数点后面一位
- 同时把余数(最好是余数)保存在hashmap里边,对应最开始的index
- 这样放(,就能直接放在了Index的位置
- 最开始的时候先把正负的符号存好

```java
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) {
            return "0";
        }
        StringBuilder res = new StringBuilder();
        // "+" or "-"
        res.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);

        // integral part
        res.append(num / den);
        num %= den;
        if (num == 0) {
            return res.toString();
        }

        // fractional part
        res.append(".");
        HashMap<Long, Integer> map = new HashMap<Long, Integer>();
        map.put(num, res.length());
        while (num != 0) {
            num *= 10;
            res.append(num / den);
            num %= den;
            if (map.containsKey(num)) {
                int index = map.get(num);
                res.insert(index, "(");
                res.append(")");
                break;
            }
            else {
                map.put(num, res.length());
            }
        }
        return res.toString();
    }
}
```
