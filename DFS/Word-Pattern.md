##Word Pattern

  Given a pattern and a string str, find if str follows the same pattern.

  Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

##Example

  Given pattern = "abba", str = "dog cat cat dog", return true.
  Given pattern = "abba", str = "dog cat cat fish", return false.
  Given pattern = "aaaa", str = "dog cat cat dog", return false.
  Given pattern = "abba", str = "dog dog dog dog", return false.

##Notice

  You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.
  
##思路
- 注意下面这种情况
- 需要两个map，或者一个map 和一个char[26]

```
"abba"
"dog dog dog dog"
```

```java
public class Solution {
    /**
     * @param pattern: a string, denote pattern string
     * @param teststr: a string, denote matching string
     * @return: an boolean, denote whether the pattern string and the matching string match or not
     */
    public boolean wordPattern(String pattern, String teststr) {
        // write your code here
        
        String[] texts = teststr.split(" ");
        
        if (texts.length != pattern.length()) {
            return false;
        }
        
        Map<Character, String> char_to_string = new HashMap<Character, String>();
        Map<String, Character> string_to_char = new HashMap<String, Character>();
        
        for (int i = 0; i < texts.length; i++) {
            
            char c = pattern.charAt(i);
            String text = texts[i];
            if (char_to_string.containsKey(c)) {
                if (!char_to_string.get(c).equals(text)) {
                    return false;
                }
            } else {
                char_to_string.put(c, text);
            }
            
            if (string_to_char.containsKey(text)) {
                if (!string_to_char.get(text).equals(c)) {
                    return false;
                }
            } else {
                string_to_char.put(text, c);
            }
        }
        
        return true;
    }
}
```
