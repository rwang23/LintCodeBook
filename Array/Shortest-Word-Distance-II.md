##Shortest Word Distance II

	Total Accepted: 5833 Total Submissions: 16718 Difficulty: Medium
	This is a follow up of Shortest Word Distance. The only difference is now you are given the list of words and your method will be called repeatedly many times with different parameters. How would you optimize it?

	Design a class which receives a list of words in the constructor, and implements a method that takes two words word1 and word2 and return the shortest distance between these two words in the list.

	For example,
	Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

	Given word1 = “coding”, word2 = “practice”, return 3.
	Given word1 = "makes", word2 = "coding", return 1.

	Note:
	You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

####思路
- I 的加强版
- 现在无非就是要有记忆化,也就是加上hashmap

```java
public class WordDistance {

    HashMap<String, ArrayList<Integer>> map = new HashMap<String, ArrayList<Integer>>();
    public WordDistance(String[] words) {
        int size = words.length;
        for (int i = 0; i < size; i++) {
            if (map.containsKey(words[i])) {
                ArrayList<Integer> list = map.get(words[i]);
                list.add(i);
                map.put(words[i], list);
            } else {
                ArrayList<Integer> list = new ArrayList<Integer>();
                list.add(i);
                map.put(words[i], list);
            }
        }
    }

    public int shortest(String word1, String word2) {
        ArrayList<Integer> list1 = map.get(word1);
        ArrayList<Integer> list2 = map.get(word2);
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

// Your WordDistance object will be instantiated and called as such:
// WordDistance wordDistance = new WordDistance(words);
// wordDistance.shortest("word1", "word2");
// wordDistance.shortest("anotherWord1", "anotherWord2");
```
