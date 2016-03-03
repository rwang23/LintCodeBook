##Shortest Word Distance

	Total Accepted: 8471 Total Submissions: 18545 Difficulty: Easy
	Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

	For example,
	Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

	Given word1 = “coding”, word2 = “practice”, return 3.
	Given word1 = "makes", word2 = "coding", return 1.

	Note:
	You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

####思路
- 先找到位置,再用两个指针

```java
public class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
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
        while (i < size1 && j < size2) {
            min = Math.min(min, Math.abs(list1.get(i) - list2.get(j)));
            if (list1.get(i) >= list2.get(j)) {
                j++;
            } else {
                i++;
            }
        }
        return min;


    }
}
```
