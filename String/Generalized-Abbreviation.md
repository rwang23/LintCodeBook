##Generalized Abbreviation
	Total Accepted: 3754 Total Submissions: 9459 Difficulty: Medium
	Write a function to generate the generalized abbreviations of a word.

	Example:
	Given word = "word", return the following list (order does not matter):
	["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]

####思路
- DFS
- [比我简洁更快的优化](http://www.cnblogs.com/EdwardLiu/p/5092886.html)

```java
public class Solution {
    public List<String> generateAbbreviations(String word) {

        List<String> result = new ArrayList<String>();

        if (word == null) {
            return result;
        }
        dfs(result, word, 0);
        return result;
    }

    public void dfs(List<String> result, String word, int pos) {
        if (!result.contains(word)) {
            result.add(new String(word));
        }
        String newWord = new String();
        for (int i = pos; i < word.length(); i++) {
            int index = i + 1;
            newWord = word.substring(0, i) + "1" + word.substring(i + 1, word.length());

            for (int j = 1; j <= i; j++) {
                String num = word.substring(i - j, i);
                if (num.matches("[0-9]+")) {
                    String newNum = Integer.toString((Integer.parseInt(num) + 1));
                    newWord = word.substring(0, i - j) + newNum + word.substring(i + 1, word.length());
                    index = index - j;
                }

            }
            dfs(result, newWord, index);
        }
    }


}
```
