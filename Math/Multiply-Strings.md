##Multiply Strings

	Total Accepted: 59422 Total Submissions: 254425 Difficulty: Medium
	Given two numbers represented as strings, return multiplication of the numbers as a string.

	Note:
	The numbers can be arbitrarily large and are non-negative.
	Converting the input string to integer is NOT allowed.
	You should NOT use internal library such as BigInteger.

####思路
- [参考1](https://leetcodenotes.wordpress.com/2013/10/20/leetcode-multiply-strings-大整数的字符串乘法/comment-page-1/#comment-122)
- [参考2](http://blog.csdn.net/fightforyourdream/article/details/17370495)
- 把乘法过程画出来
- 就会发现第k位结果是第i位乘以第k位的和(i + j == k)

```java

public class Solution {

	public String multiply(String num1, String num2) {
		// 先把string翻转
		String n1 = new StringBuilder(num1).reverse().toString();
		String n2 = new StringBuilder(num2).reverse().toString();

		int[] d = new int[n1.length() + n2.length()];		// 构建数组存放乘积
		for (int i = 0; i < n1.length(); i++){
			for (int j = 0; j < n2.length(); j++){
				d[i+j] += (n1.charAt(i) - '0') * (n2.charAt(j) - '0');		// 在正确位置累加乘积
			}
		}

		StringBuilder sb = new StringBuilder();
		for (int i = 0; i < d.length; i++) {
			int digit = d[i] % 10;		// 当前位
			int carry = d[i] / 10;		// 进位
			if (i + 1 < d.length) {
				d[i+1] += carry;
			}
			sb.insert(0, digit);		// prepend
		}

		// 移除前导零
		while (sb.charAt(0) == '0' && sb.length() > 1) {
			sb.deleteCharAt(0);
		}
		return sb.toString();
	}

}

```
