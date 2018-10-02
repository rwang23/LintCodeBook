##Regular Expression Matching


  Implement regular expression matching with support for '.' and '*'.

  '.' Matches any single character.
  '*' Matches zero or more of the preceding element.
  The matching should cover the entire input string (not partial).


  The function prototype should be:

  bool isMatch(string s, string p)

##Example

  isMatch("aa","a") → false
  isMatch("aa","aa") → true
  isMatch("aaa","aa") → false
  isMatch("aa", "a*") → true
  isMatch("aa", ".*") → true
  isMatch("ab", ".*") → true
  isMatch("aab", "c*a*b") → true


##解法
- DFS，考虑很多种情况，太容易出错了，应该再加上记忆化

```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "." and "*"
     * @return: A boolean
     */
    public boolean isMatch(String s, String p) {
        // write your code here
        
        return dfs(s, p, 0, 0);
    }
    
    public boolean dfs(String s, String p, int index_s, int index_p) {
        
        if (s.length() == index_s && p.length() == index_p) {
            return true;
        }
        
        if (s.length() == index_s || p.length() == index_p) {
            return false;
        }
        
        
        char schar = s.charAt(index_s);
        char pchar = p.charAt(index_p);
        boolean match = false;
        
        if (schar == pchar || pchar == '.') {
            if (index_p + 1 < p.length() && p.charAt(index_p + 1) == '*') {
                match = dfs(s, p, index_s, index_p + 2) || dfs(s, p, index_s + 1, index_p + 1);
            } else {
                match = dfs(s, p, index_s + 1, index_p + 1);
            }
        } else {
            if (pchar == '*') {
                if (index_s - 1 >= 0 && schar == s.charAt(index_s - 1)) {
                    match = dfs(s, p, index_s + 1, index_p) || dfs(s, p, index_s + 1, index_p + 1);
                }
                if (index_p - 1 >= 0 && p.charAt(index_p - 1) == '.') {
                    match = dfs(s, p, index_s + 1, index_p) || dfs(s, p, index_s + 1, index_p + 1);
                }
            } else {
                if (index_p + 1 < p.length() && p.charAt(index_p + 1) == '*') {
                    match = dfs(s, p, index_s, index_p + 2);
                }
            }
        }
        
        return match;
    }
}
```


###记忆化

```javapublic class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "." and "*"
     * @return: A boolean
     */
    public boolean isMatch(String s, String p) {
        if (s == null || p == null) {
            return false;
        }
        
        boolean[][] memo = new boolean[s.length()][p.length()];
        boolean[][] visited = new boolean[s.length()][p.length()];
        
        return isMatchHelper(s, 0, p, 0, memo, visited);
    }
    
    private boolean isMatchHelper(String s, int sIndex,
                                  String p, int pIndex,
                                  boolean[][] memo,
                                  boolean[][] visited) {
        // "" == ""
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        if (sIndex == s.length()) {
            return isEmpty(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;
        
        // consider a* as a bundle
        if (pIndex + 1 < p.length() && p.charAt(pIndex + 1) == '*') {
            match = isMatchHelper(s, sIndex, p, pIndex + 2, memo, visited) ||
                charMatch(sChar, pChar) && isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);
        } else {
            match = charMatch(sChar, pChar) && 
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited);
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        return match;
    }
    
    private boolean charMatch(char sChar, char pChar) {
        return sChar == pChar || pChar == '.';
    }
    
    private boolean isEmpty(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i += 2) {
            if (i + 1 >= p.length() || p.charAt(i + 1) != '*') {
                return false;
            }
        }
        return true;
    }
}
```
