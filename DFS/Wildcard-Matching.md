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
  
##记忆化
- 需要建立一个sindex和pindex的hashmap,结果是true或者false
- 如果建立了这样一个object,因为是个新的object而不是Prime type或者string,使用map.containsKey就会出问题，找不到这个object
- 取而代之的是建立一个Boolean[][]二维数组，同时再建立一个visited[][]的二维数组去记录访问

```java
public class Solution {
    /**
     * @param s: A string 
     * @param p: A string includes "?" and "*"
     * @return: is Match?
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
        // 如果 p 从pIdex开始是空字符串了，那么 s 也必须从 sIndex 是空才能匹配上
        if (pIndex == p.length()) {
            return sIndex == s.length();
        }
        
        // 如果 s 从 sIndex 是空，那么p 必须全是 * 
        if (sIndex == s.length()) {
            return allStar(p, pIndex);
        }
        
        if (visited[sIndex][pIndex]) {
            return memo[sIndex][pIndex];
        }
        
        char sChar = s.charAt(sIndex);
        char pChar = p.charAt(pIndex);
        boolean match;
        
        if (pChar == '*') {
            match = isMatchHelper(s, sIndex, p, pIndex + 1, memo, visited) ||
                isMatchHelper(s, sIndex + 1, p, pIndex, memo, visited);
        } else {
            match = charMatch(sChar, pChar) &&
                isMatchHelper(s, sIndex + 1, p, pIndex + 1, memo, visited);
        }
        
        visited[sIndex][pIndex] = true;
        memo[sIndex][pIndex] = match;
        return match;
    }
    
    private boolean charMatch(char sChar, char pChar) {
        return (sChar == pChar || pChar == '?');
    }
    
    private boolean allStar(String p, int pIndex) {
        for (int i = pIndex; i < p.length(); i++) {
            if (p.charAt(i) != '*') {
                return false;
            }
        }
        return true;
    }
}
```
