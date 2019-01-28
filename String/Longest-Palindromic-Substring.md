##Longest Palindromic Substring
[lintcode](https://www.lintcode.com/problem/implement-strstr/description)

	Total Accepted: 99803 Total Submissions: 438290 Difficulty: Medium
	Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring


####思路1
- 区间型动态规划O(n2)
- Manacher O(n)但是不用去刻意掌握
- 使用substring这个函数其实是O(n)时间复杂度,所以不要直接用,而是记录下Index就好了

```java
public class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) {
            return new String();
        }

        int size = s.length();
        boolean[][] dp = new boolean[size][size];
        String longest = new String();
        int start = 0;
        int end = size - 1;

        for (int i = 0; i < size; i++) {
            dp[i][i] = true;
        }

        for (int i = 0; i + 1< size; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                start = i;
                end = i + 1;
            }
        }

        for (int len = 2; len < size; len++) {
            for (int i = 0; i + len < size; i++) {
                if (s.charAt(i) == s.charAt(i + len) && dp[i + 1][i + len - 1]) {
                    dp[i][i + len] = true;
                    start = i;
                    end = i + len;
                }
            }
        }
        longest = s.substring(start, end + 1);

        return longest;
    }
}
```

##思路2
- 基于中心点枚举的算法
- 输入"abcdzdcab", 在输入的每个字符和字符间隙放一个指针
- 第一种情况: a|b 或者 a|a 这是第一个空位,检查指针两边是否相等
- 第二种情况: abc, 指针在b上,检查a和c是否相等
- 注意substring不要写在循环里边,否则就是O(n3)时间复杂度

```java
public class Solution {
    /**
     * @param s: input string
     * @return: the longest palindromic substring
     */
    public String longestPalindrome(String s) {
        // write your code here
        if (s == null || s.equals("")) {
            return new String("");
        }

        if (s.length() == 1) {
            return new String(s);
        }

        int max = 0;
        int start = 0;
        int end = s.length();
        for (int i = 1; i <= s.length(); i++) {
            for (int range = 1; i - range >= 0 && i + range - 1 < s.length(); range++) {
                char c1 = s.charAt(i - range);
                char c2 = s.charAt(i + range - 1);
                if (c1 == c2) {
                    if (max < range * 2) {
                        max = range * 2;
                        start = i - range;
                        end = i + range - 1;
                    }
                } else {
                    break;
                }
            }

            for (int range = 1; i - range >= 0 && i + range < s.length(); range++) {
                char c1 = s.charAt(i - range);
                char c2 = s.charAt(i + range);
                if (c1 == c2) {
                    if (max < range * 2 + 1) {
                        max = range * 2 + 1;
                        start = i - range;
                        end = i + range;
                    }
                } else {
                    break;
                }
            }
        }
        return s.substring(start, end + 1);
    }
}
```

###思路3
- 基于中心点枚举的算法
- 只不过用了两次循环,没有必要真的加入虚拟index,那样容易弄乱

```Java
public class Solution {
    /**
     * @param s: input string
     * @return: the longest palindromic substring
     */
    public String longestPalindrome(String s) {
        // write your code here
        if (s.equals("")) {
            return new String("");
        }

        int longestLength = 0;
        int start = 0;
        int end = s.length() - 1;

        for (int i = 0; i < s.length(); i++) {

            int j = 0;
            while (i - j >= 0 && i + j < s.length() && s.charAt(i - j) == s.charAt(i + j)) {
                if (longestLength < 2 * j + 1) {
                    longestLength = 2 * j + 1;
                    start = i - j;
                    end = i + j;
                }
                j++;
            }

            j = 0;
            while (i - j - 1 >= 0 && i + j < s.length() && s.charAt(i - j - 1) == s.charAt(i + j)) {
                if (longestLength < 2 * j + 2) {
                    longestLength = 2 * j + 2;
                    start = i - j - 1;
                    end = i + j;
                }
                j++;
            }

        }
        System.out.println(start);
        System.out.println(end + 1);
        return s.substring(start, end + 1);
    }
}
```
