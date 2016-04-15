##Flip Game II

	Total Accepted: 7792 Total Submissions: 18987 Difficulty: Medium
	You are playing the following Flip Game with your friend:
	Given a string that contains only these two characters: + and -,
	you and your friend take turns to flip two consecutive "++" into "--".
	The game ends when a person can no longer make a move and therefore the other person will be the winner.

	Write a function to determine if the starting player can guarantee a win.

	For example, given s = "++++", return true. The starting player can guarantee a win by flipping the middle "++" to become "+--+".

	Follow up:
	Derive your algorithm's runtime complexity.

####思路
- 递归从逻辑触发

```java
public class Solution {
    public boolean canWin(String s) {
        if (s == null || s.length() == 1) {
            return false;
        }
        return dfs(s);
    }

    public boolean dfs(String s) {

        int n = s.length();
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                String string = s.substring(0, i) + "--" + s.substring(i + 2, n);
                if (!dfs(string)) {
                    return true;
                }
            }
        }

        return false;
    }
}
```

####Memorization优化
```java
public class Solution {
    public boolean canWin(String s) {
        if (s == null || s.equals("")) {
            return false;
        }
        HashMap<String, Boolean> map = new HashMap<String, Boolean>();
        return dfs(s, map);
    }

    public boolean dfs(String s, HashMap<String, Boolean> map) {
        if (map.containsKey(s)) {
            return map.get(s);
        }

        int size = s.length();

        for (int i = 0; i < size - 1; i++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                String replaceString = s.substring(0, i) + "--" + s.substring(i + 2, size);
                if (!dfs(replaceString, map)) {
                    map.put(s, true);
                    return true;
                }
            }
        }
        map.put(s, false);
        return false;
    }
}
```
