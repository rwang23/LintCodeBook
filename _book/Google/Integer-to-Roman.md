##Integer to Roman

40% Accepted

	Given an integer, convert it to a roman numeral.

	The number is guaranteed to be within the range from 1 to 3999.

	Have you met this question in a real interview? Yes
	Example
	4 -> IV

	12 -> XII

	21 -> XXI

	99 -> XCIX

	more examples at: http://literacy.kent.edu/Minigrants/Cinci/romanchart.htm

####Clarification
	What is Roman Numeral?

	https://en.wikipedia.org/wiki/Roman_numerals
	https://zh.wikipedia.org/wiki/%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97
	http://baike.baidu.com/view/42061.htm

####Tags Expand
- String


####思路
- 创建一个表把他们存起来,总共就这么些,注意40,9,4这种别忘了相当于一个hashtable
- 每次减大的

```java
public class Solution {
    public String intToRoman(int num) {
        String[] symbols = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        StringBuilder ret = new StringBuilder();
        for (int i = 0; i < values.length; i++) {
            while (num >= values[i]) {
                ret.append(symbols[i]);
                num -= values[i];
            }
        }
        return new String(ret);
    }
}
```
