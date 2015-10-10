Word Ladder

22% Accepted

	Given two words (start and end), and a dictionary, find the length of shortest transformation sequence from start to end, such that:

	Only one letter can be changed at a time
	Each intermediate word must exist in the dictionary
	Have you met this question in a real interview? Yes
	Example
	Given:
	start = "hit"
	end = "cog"
	dict = ["hot","dot","dog","lot","log"]
	As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
	return its length 5.

	Note
	Return 0 if there is no such transformation sequence.
	All words have the same length.
	All words contain only lowercase alphabetic characters.

```java
public class Solution {
    /**
      * @param start, a string
      * @param end, a string
      * @param dict, a set of string
      * @return an integer
      */
    public int ladderLength(String start, String end, Set<String> dict) {
        LinkedList<String> queue = new LinkedList<String>();
        queue.add(start);
        dict.add(end);
        int step = 0;

        while (!queue.isEmpty()) {
            LinkedList<String> level = new LinkedList<String>();
            step++;
            while (!queue.isEmpty()) {
                String q = queue.poll();
                if (q.equals(end)) {
                    return step;
                }

                char[] t = q.toCharArray();
                for(int i = 0; i < start.length(); i++) {
                    for(char c = 'a'; c <= 'z'; c++) {
                        char temp = t[i];
                        t[i] = c;
                        String s = String.copyValueOf(t);
                        t[i] = temp;
                        if(dict.contains(s)) {
                            level.add(s);
                            dict.remove(s);
                        }
                    }
                }
            }
            queue = level;
        }
        return 0;
    }
}

```
