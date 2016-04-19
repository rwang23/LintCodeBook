##Group Anagrams

	Total Accepted: 68964 Total Submissions: 256257 Difficulty: Medium
	Given an array of strings, group anagrams together.

	For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"],
	Return:

	[
	  ["ate", "eat","tea"],
	  ["nat","tan"],
	  ["bat"]
	]
	Note:
	For the return value, each inner list's elements must follow the lexicographic order.
	All inputs will be in lower-case.

####思路
- 使用hashmap
- Map<String, List<String>>

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new ArrayList<List<String>>();
        if (strs == null || strs.length == 0) {
            return result;
        }

        Map<String, List<String>> map = new HashMap<String, List<String>>();

        for (String s : strs) {
            char[] charArray = s.toCharArray();
            Arrays.sort(charArray);
            String newS = new String(charArray);
            if (!map.containsKey(newS)) {
                List<String> list = new ArrayList<String>();
                list.add(s);
                map.put(newS, list);
            } else {
                map.get(newS).add(s);
            }
        }

        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            List<String> list = entry.getValue();
            Collections.sort(list);
            result.add(list);
        }

        return result;
    }
}
```
