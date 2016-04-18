##Alien Dictionary

	Total Accepted: 7299 Total Submissions: 31880 Difficulty: Hard
	There is a new alien language which uses the latin alphabet.
	However, the order among letters are unknown to you.
	You receive a list of words from the dictionary, where words are sorted lexicographically by the rules of this new language.
	Derive the order of letters in this language.

	For example,
	Given the following words in dictionary,

	[
	  "wrt",
	  "wrf",
	  "er",
	  "ett",
	  "rftt"
	]
	The correct order is: "wertf".

	Note:
	You may assume all letters are in lowercase.
	If the order is invalid, return an empty string.
	There may be multiple valid order of letters, return any one of them is fine.

####思路
- 构造图,然后根据入度进行topological sort
- 但是关键是,注意要进行判断,是否是valid的顺序,如果存在环,那么就是invalid,可以通过当queue已经为空的时候,还有入度(没被删除)
- 具体见代码与注释

```java
public class Solution {
    public String alienOrder(String[] words) {
        if (words == null || words.length == 0) {
            return new String();
        }
        //if there is only one word, it's not invalid, but we don't know the exact order
        if (words.length == 1) {
            return words[0];
        }

        Map<Character, List<Character>> map = new HashMap<>();
        StringBuilder sb = new StringBuilder();
        int size = words.length;

        //build graph
        for (int i = 0; i < size - 1; i++) {
            String first = words[i];
            String second = words[i + 1];
            int index1 = 0;
            int index2 = 0;

            //find edges
            while (index1 < first.length() && index2 < second.length()) {
                char c1 = first.charAt(index1);
                char c2 = second.charAt(index2);
                if (!map.containsKey(c1)) {
                    List<Character> list = new ArrayList<>();
                    map.put(c1, list);
                }
                if (c1 == c2) {
                    index1++;
                    index2++;
                    continue;
                }

                if (!map.containsKey(c2)) {
                    List<Character> list = new ArrayList<>();
                    map.put(c2, list);
                }
                map.get(c1).add(c2);

                //if the order has conflict, return ""
                if (map.get(c2).contains(c1)) {
                    return new String();
                }
                break;
            }

            //add neighbor
            while (index1 < first.length()) {
                char c1 = first.charAt(index1++);
                if (!map.containsKey(c1)) {
                    List<Character> list = new ArrayList<>();
                    map.put(c1, list);
                }
            }
            //add neighbor
            while (index2 < second.length()) {
                char c2 = second.charAt(index2++);
                if (!map.containsKey(c2)) {
                    List<Character> list = new ArrayList<>();
                    map.put(c2, list);
                }
            }
        }

        //get indegrees
        Map<Character, Integer> indegree = new HashMap<>();
        for (Map.Entry<Character, List<Character>> entry : map.entrySet()) {
            char key = entry.getKey();
            List<Character> value = entry.getValue();
            if (!indegree.containsKey(key)) {
                indegree.put(key, 0);
            }

            for (Character c : value) {
                if (!indegree.containsKey(c)) {
                    indegree.put(c, 1);
                } else {
                    indegree.put(c, indegree.get(c) + 1);
                }
            }
        }

        //find node whose indegrees == 0
        Queue<Character> queue = new LinkedList<>();
        for (Map.Entry<Character, Integer> entry : indegree.entrySet()) {
            char key = entry.getKey();
            int degree = entry.getValue();
            if (degree == 0) {
                queue.offer(key);
            }
        }

        //BFS
        StringBuilder result = new StringBuilder();
        while (!queue.isEmpty()) {
            char start = queue.poll();
            result.append(start);
            List<Character> neighbors = map.get(start);

            for (Character neighbor : neighbors) {
                // if (indegree.get(neighbor) == 0) {
                //     continue;
                // }

                indegree.put(neighbor, indegree.get(neighbor) - 1);
                if (indegree.get(neighbor) == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        //if queue is empty but there still is indegree, then this is invalid
        for (Map.Entry<Character, Integer> entry : indegree.entrySet()) {
            char key = entry.getKey();
            int degree = entry.getValue();
            if (degree != 0) {
                return new String();
            }
        }


        return result.toString();
    }
}
```
