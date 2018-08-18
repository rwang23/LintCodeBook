##Longest Palindrome
[lintcode](https://www.lintcode.com/problem/longest-palindrome/description)

	Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

	This is case sensitive, for example "Aa" is not considered a palindrome here.

##Example
	Given s = "abccccdd" return 7

	One longest palindrome that can be built is "dccaccd", whose length is 7.

	Notice
	Assume the length of given string will not exceed 1010.

##思路
- 一开始用了map
- 后来一想只需要set,每次put然后在遇到remove

```java
public class Solution {
    /**
     * @param s: a string which consists of lowercase or uppercase letters
     * @return: the length of the longest palindromes that can be built
     */
    public int longestPalindrome(String s) {
        // write your code here
        if (s == null || s.equals("")) {
            return 0;
        }

        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (map.containsKey(c)) {
                map.put(c, map.get(c) + 1);
            } else {
                map.put(c, 1);
            }
        }

        int sum = 0;
        boolean hasOdd = false;
        for (Integer i : map.values()) {
            if (i % 2 == 0) {
                sum += i;
            } else {
                sum += i - 1;
                hasOdd = true;
            }
        }

        if (hasOdd) {
            sum++;
        }
        return sum;
    }
}
```

```java
public class Solution {
    /**
     * @param s a string which consists of lowercase or uppercase letters
     * @return the length of the longest palindromes that can be built
     */
    public int longestPalindrome(String s) {
        // Write your code here
        Set<Character> set = new HashSet<>();
        for (char c : s.toCharArray()) {
            if (set.contains(c)) set.remove(c);
            else set.add(c);
        }

        int remove = set.size();
        if (remove > 0)
            remove -= 1;
        return s.length() - remove;
    }
}
```
