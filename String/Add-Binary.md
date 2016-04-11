##Add Binary

	Total Accepted: 80998 Total Submissions: 297347 Difficulty: Easy
	Given two binary strings, return their sum (also a binary string).

	For example,
	a = "11"
	b = "1"
	Return "100".

####思路
- 从后读取字符,硬做
- 利用append,然后再reverse,这样比insert快很多

```java
public class Solution {
    public String addBinary(String a, String b) {
        int m = a.length() - 1;
        int n = b.length() - 1;
        int minLen = Math.min(m, n);
        int carry = 0;
        StringBuilder string = new StringBuilder();
        while (minLen >= 0) {
            minLen--;
            int num1 = a.charAt(m--) - '0';
            int num2 = b.charAt(n--) - '0';
            int sum = num1 + num2 + carry;
            carry = sum / 2;
            sum = sum % 2;
            string.append(sum);
        }

        while (m >= 0) {
            int num = a.charAt(m--) - '0';
            int sum = num + carry;
            carry = sum / 2;
            sum = sum % 2;
            string.append(sum);
        }
        while (n >= 0) {
            int num = b.charAt(n--) - '0';
            int sum = num + carry;
            carry = sum / 2;
            sum = sum % 2;
            string.append(sum);
        }
        if (carry != 0) {
            string.append(carry);
        }
        char[] array = string.toString().toCharArray();
        for (int i = 0, j = array.length - 1; i < j; i++, j--) {
            char temp = array[i];
            array[i] = array[j];
            array[j] = temp;
        }

        return new String(array);
    }
}
```
