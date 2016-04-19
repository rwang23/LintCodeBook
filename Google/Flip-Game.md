##Flip Game

	Total Accepted: 7521 Total Submissions: 15233 Difficulty: Easy
	You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

	Write a function to compute all possible states of the string after one valid move.

	For example, given s = "++++", after one move, it may become one of the following states:

	[
	  "--++",
	  "+--+",
	  "++--"
	]
	If there is no valid move, return an empty list [].

####思路
- 很简单,换++为--

```java
public class Solution {
    public List<String> generatePossibleNextMoves(String s) {
        List<String> result = new ArrayList<String>();
        if (s == null || s.length() == 1) {
            return result;
        }
        int n = s.length();

        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+') {
                String string = s.substring(0, i) + "--" + s.substring(i + 2, n);
                result.add(string);
            }
        }
        return result;
    }
}
```
