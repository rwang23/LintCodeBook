##Shortest Palindrome
	Total Accepted: 18753 Total Submissions: 95420 Difficulty: Hard
	Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

	For example:

	Given "aacecaaa", return "aaacecaaa".

	Given "abcd", return "dcbabcd".

####思路
- step1 扩展点,每个点有个空格
- step2 找每个点周围最多相等的点的数量
- step3 找最大的数量
- step4 找最大数量的点
- step5 extend stringbuilder
- step6 combine
- O(n2)
- leetcode超时,IDE能跑出来

```java
public class Solution {
    public String shortestPalindrome(String s) {
        if (s == null || s.equals("")) {
            return new String();
        }

        int size = s.length();
        int newLen = size * 2;
        char[] chars = new char[newLen];
        chars[0] = ' ';
        for (int i = 0; i < size - 1; i++) {
            chars[2 * i + 1] = s.charAt(i);
            chars[2 * i + 2] = ' ';
        }
        chars[size * 2 - 1] = s.charAt(size - 1);

        int[] nums = new int[newLen];
        for (int i = 1; i < newLen - 1; i++) {
            for (int len = 1; i + len < newLen && i - len >= 0; len++) {
                char before = chars[i - len];
                char after = chars[i + len];
                if (before == after) {
                    nums[i] = nums[i] + 1;
                } else {
                    break;
                }
            }
        }
        nums[0] = 1;
        int max = 0;
        for (int i = 0; i < newLen; i++) {
            if (nums[i] > max) {
                max = nums[i];
            }
        }
        int index = 0;
        for (int i = 0; i < newLen; i++) {
            if (nums[i] == max) {
                index = i;
                break;
            }
        }

        StringBuilder sb = new StringBuilder();

        for (int i = newLen - 1; i > index + max; i--) {
            if (chars[i] != ' ') {
                sb.append(chars[i]);
            }
        }

        return sb.toString() + s;

    }
}
```

####O(n) KMP
- [很棒的视频](https://www.youtube.com/watch?v=c4akpqTwE5g)
- Code来自九章

```java
public class Solution {

    public String shortestPalindrome(String s) {

        int j = 0;
        for (int i = s.length() - 1; i >= 0; i--) {//找到第一个使他不回文的位置
           if (s.charAt(i) == s.charAt(j)) {
               j += 1;
           }
        }

        if (j == s.length()) {  //本身是回文
            return s;
        }

        String suffix = s.substring(j); // 后缀不能够匹配的字符串
        String prefix = new StringBuilder(suffix).reverse().toString(); // 前面补充prefix让他和suffix回文匹配
        String mid = shortestPalindrome(s.substring(0, j)); //递归调用找 [0,j]要最少可以补充多少个字符让他回文
        String ans = prefix + mid  + suffix;
        return  ans;
    }
}
```
