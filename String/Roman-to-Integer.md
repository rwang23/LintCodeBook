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
    /**
     * @param s Roman representation
     * @return an integer
     */
    public int romanToInt(String s) {
        // Write your code here
        String[] symbols = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        HashMap<String, Integer> hashtmap = new HashMap<String, Integer>();
        for (int i = 0; i < symbols.length; i++) {
            hashtmap.put(symbols[i], values[i]);
        }
        int sum = 0;
        StringBuilder temp = new StringBuilder(s);
        temp.append("A");
        s = temp.toString();

        for (int i = 1; i < s.length();) {
            String cur = s.substring(i-1, i+1);
            if (hashtmap.containsKey(cur)) {
                sum += hashtmap.get(cur);
                i = i + 2;
                continue;
            }


            cur = s.substring(i-1, i);
            if (hashtmap.containsKey(cur)) {
                sum += hashtmap.get(cur);
            }
            i++;

        }
        return sum;
    }
}

```
