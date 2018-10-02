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
- 注意去重
- 既然有了visited，就利用visited进行判断，如果char[i] == char[i-1] 而i-1还没走过，那么一定是重复的
- permutation 里边是使用index进行去重，有了visted就更容易

```java
public class Solution {
    /**
     * @param str: A string
     * @return: all permutations
     */
    public List<String> stringPermutation2(String str) {
        // write your code here
        List<String> results = new ArrayList<String>();
        
        if (str == null || str.length() == 0) {
            results.add("");
            return results;
        }
        
        boolean[] visited = new boolean[str.length()];
        char[] chars = str. toCharArray();
        Arrays.sort(chars);
        
        helper(results, visited, chars, new StringBuilder(""));
        
        return results;
    }
    
    public void helper(List<String> results, boolean[] visited, char[] chars, StringBuilder sb) {
        
        if (sb.length() == chars.length) {
            String target = sb.toString();
            results.add(target);
            return;
        }
        
        for (int i = 0; i < chars.length; i++) {
            if (visited[i]) {
                continue;
            }
            
            if (i >= 1 && chars[i] == chars[i - 1] && !visited[i - 1]) {
                continue;
            }
            
            sb.append(chars[i]);
            visited[i] = true;
            helper(results, visited, chars, sb);
            visited[i] = false;
            sb.setLength(sb.length() - 1);
        }
    }
}
```
