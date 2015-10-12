Word Break

12% Accepted

	Given a string s and a dictionary of words dict, determine if s can be break into a space-separated sequence of one or more dictionary words.

	Have you met this question in a real interview? Yes
	Example
	Given s = "lintcode", dict = ["lint", "code"].

	Return true because "lintcode" can be break as "lint code".

####Tags Expand
- String
- Dynamic Programming

####思路
- Sequence DP
- 自己图都画好了，但是条件写错了，就按照自己图写就行

```java
public class Solution {
    /**
     * @param s: A string s
     * @param dict: A dictionary of words dict
     */
    public boolean wordBreak(String s, Set<String> dict) {
        // write your code here

        int maxLength = 0;

        //cannot use get in Set class
        for (String word : dict) {
            maxLength = Math.max(maxLength, word.length());
        }
        if (s == null || s.length() == 0) {
            return true;
        }
        if (dict == null) {
            return false;
        }

        boolean[] canBreak = new boolean[s.length()+1];
        canBreak[0] = true;

        for (int i = 1; i <= s.length(); i++) {
            canBreak[i] = false;
            for (int j = 1; j <= Math.min(i, maxLength); j++) {
                if (!canBreak[i - j]) {
                    continue;
                }
                if (dict.contains(s.substring(i - j, i))) {
                    canBreak[i] = true;
                    break;
                }
            }
        }

        return canBreak[s.length()];
    }
}

```
