##ZigZag Conversion

	Total Accepted: 82829 Total Submissions: 348776 Difficulty: Easy
	The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this:
	(you may want to display this pattern in a fixed font for better legibility)

	P   A   H   N
	A P L S I I G
	Y   I   R
	And then read line by line: "PAHNAPLSIIGYIR"
	Write the code that will take a string and make this conversion given a number of rows:

	string convert(string text, int nRows);
	convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

####思路
- 直接做
- 看这个[图](https://leetcode.com/discuss/55208/if-you-are-confused-with-zigzag-pattern-come-and-see)理解zigzag的含义
- 虽然有了这个图之后,思路就变得很简单了..但是很容易错
- 比如第一行最后一行要单独处理

```java
public class Solution {
    public String convert(String s, int numRows) {
        if (s == null || s.length() == 0 || numRows <= 0) {
            return new String();
        }
        if (numRows == 1 || s.length() <= numRows) {
            return s;
        }
        StringBuilder string = new StringBuilder();
        int size = s.length();
        int back = 0;

        for (int i = 0; i < numRows; i++) {
            int cur = i;
            if (i == 0 || i == numRows - 1) {
                while (cur < size) {
                    char c = s.charAt(cur);
                    string.append(c);
                    cur += 2 * numRows - 2;
                }
            } else {
                char c = s.charAt(cur);
                string.append(c);
                cur += 2 * numRows - 2 - back;
                while (cur < size) {
                    c = s.charAt(cur);
                    string.append(c);
                    cur += back;
                    if (cur < size) {
                        c = s.charAt(cur);
                        string.append(c);
                        cur += 2 * numRows - 2 - back;
                    }
                }
            }
            back = back + 2;

        }

        return string.toString();
    }
}
```
