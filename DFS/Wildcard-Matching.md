##Wildcard Matching
  Implement wildcard pattern matching with support for '?' and '*'.

  '?' Matches any single character.
  '*' Matches any sequence of characters (including the empty sequence).
  The matching should cover the entire input string (not partial).

##Example
  isMatch("aa","a") → false
  isMatch("aa","aa") → true
  isMatch("aaa","aa") → false
  isMatch("aa", "*") → true
  isMatch("aa", "a*") → true
  isMatch("ab", "?*") → true
  isMatch("aab", "c*a*b") → false
 
##思路
- DFS
- 注意?不匹配空字符
- 直接做优点超时了
- 需要一个记忆化

##无记忆化
```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
     */
    public boolean isMatch(String s, String p) {
        // write your code here
        return dfs(s, p, 0, 0);
    }
    
    public boolean dfs(String s, String p, int index_s, int index_p) {
        
        if (index_s == s.length() && index_p == p.length()) {
            return true;
        }
        
        if (index_p == p.length()) {
            return false;
        }
        
        if (index_s == s.length()) {
            char c = p.charAt(index_p);
            if (c != '*') {
                return false;
            }
            return dfs(s, p, index_s, index_p + 1);
        }
        
        char schar = s.charAt(index_s);
        char pchar = p.charAt(index_p);
        boolean match = false;
        
        if (schar == pchar) {
            match = dfs(s, p, index_s + 1, index_p + 1);
        } else {
            if (pchar == '?') {
                match = dfs(s, p, index_s + 1, index_p + 1);
            } else if (pchar == '*') {
                match = dfs(s, p, index_s + 1, index_p) || dfs(s, p, index_s, index_p + 1) || dfs(s, p, index_s + 1, index_p + 1);
            } else {
                return false;
            }
        }
        
        return match;
        
        
    }
}
```
  
