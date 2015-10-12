##Palindrome Partitioning II

20% Accepted

	Given a string s, cut s into some substrings such that every substring is a palindrome.

	Return the minimum cuts needed for a palindrome partitioning of s.

	Have you met this question in a real interview? Yes
	Example
	For example, given s = "aab",

	Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

####Tags Expand
- Dynamic Programming

####思路
- state: f[i]”前i”个字符组成的子字符串需要最少几次cut(最少能被分割为多少个字符串-1)
- function: f[i] = MIN{f[j]+1}, j < i && j+1 ~ i这一 段是一个回文串
- intialize: f[i] = i - 1 (f[0] = -1)
- answer: f[s.length()]
- 见注释

```java
public class Solution {
    /**
     * @param s a string
     * @return an integer
     */
    public int minCut(String s) {
        // write your code here
        if (s == null || s.length() == 0) {
            return 0;
        }
        // preparation
        boolean[][] result = getPalindrome(s);
        // s.length() + 1
        int[] step = new int[s.length() + 1];
        // initialize
        for (int i = 0; i <= s.length(); i++) {
            step[i] = i -1;
        }

        //i <= s.length()
        //result[j][i-1]
        //Math.min(step[j] + 1, step[i]);
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (result[j][i-1]) { // i-1
                    step[i] = Math.min(step[j] + 1, step[i]);

                }
            }
        }

        return step[s.length()];
    }

    //getPalindrome also use dynamic programming
    //otherwise the whole program will need O(n3) time
    //now it just use O(n2)
    //this is called space dynamic programming
    public boolean[][] getPalindrome(String s) {
        int len = s.length();
        boolean[][] result = new boolean[len][len];
        //initialization 1
        for (int i = 0; i < len; i++) {
            result[i][i] = true;
        }
        //initialization 2
        for (int i = 0; i < len - 1; i++) {
            result[i][i + 1] = (s.charAt(i) == s.charAt(i + 1));
        }

        for (int length = 2; length < len; length++) {
            for (int start = 0; start + length < len; start++) {
                result[start][start + length] = result[start + 1][start + length - 1] && s.charAt(start) == s.charAt(start + length);
            }
        }

        return result;
    }

        // private boolean isPalindrome(String s, int start, int end) {
    //     for (int i = start, j = end; i < j; i++, j--) {
    //         if (s.charAt(i) != s.charAt(j)) {
    //             return false;
    //         }
    //     }
    //     return true;
    // }

};

```
