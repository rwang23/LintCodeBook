##Shortest Word Distance III

	Total Accepted: 5777 Total Submissions: 12636 Difficulty: Medium
	This is a follow up of Shortest Word Distance. The only difference is now word1 could be the same as word2.

	Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

	word1 and word2 may be the same and they represent two individual words in the list.

	For example,
	Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

	Given word1 = “makes”, word2 = “coding”, return 1.
	Given word1 = "makes", word2 = "makes", return 3.

####思路
- I 稍微变形

```java
public class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        int size = words.length;

        ArrayList<Integer> list1 = new ArrayList<Integer>();
        ArrayList<Integer> list2 = new ArrayList<Integer>();

        for (int i = 0; i < size; i++) {
            if (words[i].equals(word1)) {
                list1.add(i);
            } else if (words[i].equals(word2)) {
                list2.add(i);
            }
        }

        int size1 = list1.size();
        int size2 = list2.size();
        int i = 0;
        int j = 0;
        int min = Integer.MAX_VALUE;
        if (size1 > 0 && size2 > 0) {
            while (i < size1 && j < size2) {
                min = Math.min(min, Math.abs(list1.get(i) - list2.get(j)));
                if (list1.get(i) >= list2.get(j)) {
                    j++;
                } else {
                    i++;
                }
            }
        } else {
            for (int k = 1; k < size1; k++) {
                min = Math.min(min, list1.get(k) - list1.get(k - 1));
            }
        }

        return min;

    }

}
```
