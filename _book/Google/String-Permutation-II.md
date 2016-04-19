##String Permutation II

	Given a string, find all permutations of it without duplicates.

	Have you met this question in a real interview? Yes
	Example
	Given "abb", return ["abb", "bab", "bba"].

	Given "aabb", return ["aabb", "abab", "baba", "bbaa", "abba", "baab"].

####Tags Expand
String Permutation Recursion


####思路
- 跟permutation差不多
- 但是lintcode显示我超时了,然而我在自己的eclipse跑出来没问题

```java
public class Solution {
    /**
     * @param str a string
     * @return all permutations
     */
    public List<String> stringPermutation2(String str) {
        // Write your code here
        if (str == null) {
            return new ArrayList<String>();
        }
        List<String> result= new ArrayList<String>();
        StringBuilder word = new StringBuilder();
        HashSet<Integer> set = new HashSet<Integer>();
        char[] characters = str.toCharArray();
        Arrays.sort(characters);
        dfs(result, word, characters, set);
        return result;
    }

    public void dfs(List<String> result, StringBuilder word, char[] characters, HashSet<Integer> set) {
        if (word.length() == characters.length) {
            String cur = word.toString();
            if (!result.contains(cur)) {
                result.add(new String(cur));
            }
            return;
        }

        if (word.length() >= characters.length) {
            return;
        }

        for (int i = 0; i < characters.length; i++) {
            if (set.contains(i)) {
                continue;
            }
            set.add(i);
            word.append(characters[i]);
            dfs(result, word, characters, set);
            word.deleteCharAt(word.length() - 1);
            set.remove(i);
        }
    }
}
```
