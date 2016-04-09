##Roman to Integer

40% Accepted

	Given a roman numeral, convert it to an integer.

	The answer is guaranteed to be within the range from 1 to 3999.

	Have you met this question in a real interview? Yes
	Example
	IV -> 4

	XII -> 12

	XXI -> 21

	XCIX -> 99

####Clarification
	What is Roman Numeral?

	https://en.wikipedia.org/wiki/Roman_numerals
	https://zh.wikipedia.org/wiki/%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97
	http://baike.baidu.com/view/42061.htm
####Tags Expand
- String

####思路
- 避免写很多条件,所以自己用了hashmap来存起来,先找两个字母的,找到了就加上,没找到肯定就是一个字母的
- 这里用了小trick,在string后面自己添加了一个不是罗马数字的字符,来避免越过边界的条件

```java
public class Solution {
    public int romanToInt(String s) {
        if (s == null) {
            return 0;
        }
        String[] symbols = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};

        int sum = 0;
        int j = 0;
        for (int i = 1; i <= s.length();) {
            while (j < symbols.length) {

                String cur = symbols[j];
                int size = cur.length();

                if (size == 1 && s.substring(i - 1, i).equals(symbols[j])) {
                    sum += values[j];
                    i++;
                    break;
                }

                if (i != s.length() && size == 2 && s.substring(i - 1, i + 1).equals(symbols[j])) {
                    sum += values[j];
                    i += 2;
                    break;
                }
                j++;
            }
        }

        return sum;
    }
}

```
