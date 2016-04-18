##Generalized Abbreviation
	Total Accepted: 3754 Total Submissions: 9459 Difficulty: Medium
	Write a function to generate the generalized abbreviations of a word.

	Example:
	Given word = "word", return the following list (order does not matter):
	["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]

####思路
- DFS,但是我的方法IDE跑出来没问题,但是leetcode超时了,substring太花 时间了

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

            for (int j = i; j >= 0; j--) {
                String num = word.substring(i - j, i);
                if (num.matches("[0-9]+")) {
                    String newNum = Integer.toString((Integer.parseInt(num) + 1));
                    newWord = word.substring(0, i - j) + newNum + word.substring(i + 1, word.length());
                    index = index - j;
                    break;
                }
            }
            dfs(result, newWord, index);
        }
    }
}
```

####更快的解法
- [比我简洁更快的优化](http://www.cnblogs.com/EdwardLiu/p/5092886.html)
- 针对每个char,可以选择abbr或者不abbr
- 如果要,用一个Num来记录,每次加1,然后先不append
- 如果不要abbr,直接append这个字符

```java
public class Solution {
    public List<String> generateAbbreviations(String word){
        List<String> ret = new ArrayList<String>();
        backtrack(ret, word, 0, "", 0);

        return ret;
    }

    private void backtrack(List<String> ret, String word, int pos, String cur, int count){
        if(pos==word.length()){
            if(count > 0) cur += count;
            ret.add(cur);
        }
        else{
            backtrack(ret, word, pos + 1, cur, count + 1);
            backtrack(ret, word, pos + 1, cur + (count>0 ? count : "") + word.charAt(pos), 0);
        }
    }
}
```

####Bits Map
- [参考](http://algobox.org/generalized-abbreviation/)

```
For each character they ends up two ways in the abbreviation, they either appear as it is, or they contribute to the number.

Therefore for a word of length n, there will be 2^n combinations.

Each of these combination can be represented by a binary number of n bit.
Since the problem require to return all the abbreviations, n needs to be relatively small, otherwise the return list can be huge. Therefore we assume n < 32 and use 32 bit int to represent the combination. If it is not enough we can use long instead or we can use backtracking to generate whatever length.

The remaining problem is applying the bit mask and generate the abbreviation. In short, we can scan all the bits of the mask and append the character when corresponding bit is 0 and the count of bit 1 before that.
```

