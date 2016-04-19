##Integer to English Words

	Total Accepted: 14526 Total Submissions: 78121 Difficulty: Hard
	Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than 231 - 1.

	For example,
	123 -> "One Hundred Twenty Three"
	12345 -> "Twelve Thousand Three Hundred Forty Five"
	1234567 -> "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"

####思路
- 因为数字在英语中是三位三位出现的,100,000这种,所以三位是一个文字单元
- 每三位才会出现一个 hundred,thousand,million这种
- 所以分了两部处理,一个是处理三位数字,一个是处理三位数字后跟thousand,还是million

```java
public class Solution {

    String[] map1 = new String [] {"", " One", " Two", " Three", " Four", " Five",
            " Six", " Seven", " Eight", " Nine", " Ten", " Eleven", " Twelve",
            " Thirteen", " Fourteen", " Fifteen", " Sixteen", " Seventeen",
            " Eighteen", " Nineteen" };

    String[] map2 = new String[] {"", "", " Twenty", " Thirty", " Forty", " Fifty", " Sixty",
        " Seventy", " Eighty", " Ninety" };

    String[] map3 = new String[] {"", " Thousand", " Million", " Billion" };
    final String HUNDRED = " Hundred";

    public String threeDigitToWords(int num) {
        String result = "";
        if (num > 99) {
            result = map1[num / 100] + HUNDRED;
        }
        num %= 100;
        if (num < 20) {
            result +=  map1[num];
        }else {
            result += map2[num/10] + map1[num%10];
        }
        return result;
    }

    public String numberToWords(int num) {
        if (num == 0) return "Zero";
        String result = "";

        int i = 0; //check if it is thousand, million, billion
        while (num != 0) {
            if (num % 1000 != 0) {
                result = threeDigitToWords(num % 1000) + map3[i] + result;
            }
            i++;
            num /= 1000;
        }
        return result.trim();
    }
}

```
