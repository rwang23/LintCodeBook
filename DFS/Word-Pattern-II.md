##Word Pattern II

  Given a pattern and a string str, find if str follows the same pattern.

  Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty substring in str.(i.e if a corresponds to s, then b cannot correspond to s. For example, given pattern = "ab", str = "ss", return false.)

##Example

  Given pattern = "abab", str = "redblueredblue", return true.
  Given pattern = "aaaa", str = "asdasdasdasd", return true.
  Given pattern = "aabb", str = "xyzabcxzyabc", return false.

##Notice
  You may assume both pattern and str contains only lowercase letters.
  
  
##思路
- DFS
- 有个case没过..没找出来原因

```java
public class Solution {
    /**
     * @param pattern: a string,denote pattern string
     * @param str: a string, denote matching string
     * @return: a boolean
     */
    public boolean wordPatternMatch(String pattern, String str) {
        // write your code here
        
        Map<Character, String> char_to_string = new HashMap<Character, String>();
        Map<String, Character> string_to_char = new HashMap<String, Character>();
        
        return dfs(char_to_string, string_to_char, pattern, str, 0, 0);
        
    }
    
    public boolean dfs(Map<Character, String> char_to_string, Map<String, Character> string_to_char, String pattern, String str, int pIndex, int sIndex) {
        if (pIndex == pattern.length() && sIndex == str.length()) {
            return true;
        }
        
        if (pIndex == pattern.length() || sIndex == str.length()) {
            return false;
        }
        
        char c = pattern.charAt(pIndex);
        
        for (int i = sIndex + 1; i <= str.length(); i++) {
            String substr = str.substring(sIndex, i);
            boolean isMatched = false;

            if (char_to_string.containsKey(c)) {
                if (!char_to_string.get(c).equals(substr)) {
                    continue;
                }
            } else {
                char_to_string.put(c, substr);
                putChar = true;
            }
            
            
            if (string_to_char.containsKey(substr)) {
                if (!string_to_char.get(substr).equals(c)) {
                    continue;
                }
            } else {
                string_to_char.put(substr, c);
                putSubstring = true;
            }
            
            
            isMatched = dfs(char_to_string, string_to_char, pattern, str, pIndex + 1, i);
            if (isMatched) {
                return isMatched;
            }
            
            if (putChar) {
                char_to_string.remove(c);
            }
            
            if (putSubstring) {
                string_to_char.remove(substr);
            }
        }
        
        return false;
        
    }
}
```

##可以过得版本
```java
public class Solution {
    /**
     * @param pattern: a string,denote pattern string
     * @param str: a string, denote matching string
     * @return: a boolean
     */
    public boolean wordPatternMatch(String pattern, String str) {
        Map<Character, String> map = new HashMap<>();
        return dfs(pattern, str, map);
    }
    
    private boolean dfs(String ptn, String s, Map<Character, String> map) {
        if (ptn.length() == 0 && s.length() == 0) {
            return true;
        }
        
        if (ptn.length() == 0 || s.length() == 0) {
            return false;
        }
        
        if (map.containsKey(ptn.charAt(0))) {
            String prefix = map.get(ptn.charAt(0));
            if (!s.startsWith(prefix)) {
                return false;
            }
            return dfs(ptn.substring(1), s.substring(prefix.length()), map);
        }
        
        for (int i = 1; i <= s.length(); i++) {
            String prefix = s.substring(0, i);
            if (map.values().contains(prefix)) {
                continue;
            }
            map.put(ptn.charAt(0), prefix);
            if (dfs(ptn.substring(1), s.substring(prefix.length()), map)) {
                return true;
            }
            map.remove(ptn.charAt(0));
        }
        return false;
    }
}
```
