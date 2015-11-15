##Minimum Window Substring

20% Accepted

	Given a string source and a string target, find the minimum window in source which will contain all the characters in target.

	Have you met this question in a real interview? Yes
	Example
	source = "ADOBECODEBANC" target = "ABC" Minimum window is "BANC".

	Note
	If there is no such window in source that covers all characters in target, return the emtpy string "".

	If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in source.

	Challenge
	Can you do it in time complexity O(n) ?

####Clarification
Should the characters in minimum window has the same order in target?

    - Not necessary.

####Tags Expand
- Hash Table


####暴力解法 O(k*n2)
- 使用HashMap<Character, Integer>去判断
- 先将target 的字母,和字母出现次数 放入哈希表
- 是否这个字母满足了,是的话,integer -1

```java
public class Solution {
    /**
     * @param source: A string
     * @param target: A string
     * @return: A string denote the minimum window
     *          Return "" if there is no such a string
     */
    public String minWindow(String source, String target) {
        // write your code
        if (source.length() == 0 || target.length() == 0 || source.length() < target.length()) {
            return new String("");
        }

        int size = source.length();
        String result = "";
        int min = Integer.MAX_VALUE;
        HashMap<Character, Integer> hashmap = new HashMap<Character, Integer>();
        for (int k = 0; k < target.length(); k++) {
            if (!hashmap.containsKey(target.charAt(k))) {
                hashmap.put(target.charAt(k), 1);
            } else {
                hashmap.put(target.charAt(k), hashmap.get(target.charAt(k)) + 1);
            }
        }

        for (int i = 0; i < size; i++) {
            HashMap<Character, Integer> copy = new HashMap<Character, Integer>(hashmap);
            int count = 0;
            for (int j = i; j < size; j++) {
                char key = source.charAt(j);
                if(copy.containsKey(key)) {
                    copy.put(key, hashmap.get(key) - 1);
                }
                count++;
                if(isValid(copy, target)) {
                    min = Math.min(min, count);
                    if (min == count) {
                        result = source.substring(i,j+1);
                    }
                    break;
                }

            }
        }
        return result;
    }

    public boolean isValid(HashMap<Character, Integer> hashmap, String target) {
        boolean valid = true;
        for (int i = 0; i < target.length(); i++) {
            if (hashmap.get(target.charAt(i)) > 0 ) {
                valid = false;
                break;
            }
        }
        return valid;
    }
}

```

####优化解法
