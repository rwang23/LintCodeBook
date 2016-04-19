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
- 把 char key = target.charAt(k) 单独写出来,否则 hashmap.containsKey(target.charAt(k)), 特别是些hashmap.put的时候太容易出低级bug
- [0,6] --> 不需要找[0,7], 去找[1,6],如果[1,6]不行,再[1,7]
- 这样的两根指针优化,常常用在,可以直接想到i,j两重循环去做,然后去思考是不是可以忽略一些情况,就变成两根指针同时前进,优化少掉一层负责度数量级

- 前向型双指针,只需要变i,而j不变,因为[i,j]如果刚好是可包含targat的串,[i,j+1]肯定也是,[i+1,j][i+2,j]等等肯定不是,此时j才继续向前进
- 设置hashmap来存target
- 设置一个copy来保存现在的状态
- 注意将map赋值到copy的时候,要创建新的,不然还是一个内存的位置
- 并且不用去存这段string,去存开始的index和结尾的index就好了

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
        if (source == null || target == null || source.length() < target.length()) {
            return new String("");
        }

        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        StringBuilder process = new StringBuilder("");
        String result = new String("");

        for (int i = 0; i < target.length(); i++) {
            char cur = target.charAt(i);
            if (map.containsKey(cur)) {
                map.put(cur, map.get(cur) + 1);
            } else {
                map.put(cur, 1);
            }
        }

        int i = 0;
        int j = 0;
        int min = Integer.MAX_VALUE;
        HashMap<Character, Integer> copy = new HashMap<Character, Integer>(map);

        for (i = 0; i < source.length(); i++) {

            while (valid(copy) && j < source.length()) {
                char cur = source.charAt(j++);
                if (copy.containsKey(cur)) {
                    copy.put(cur, copy.get(cur) - 1);
                }
                process.append(cur);
            }

            if (!valid(copy)) {
                min = Math.min(min, process.length());
                if (min == process.length()) {
                    result = process.toString();
                }
            }
            process.deleteCharAt(0);
            char curchar = source.charAt(i);
            if (map.containsKey(curchar)) {
                if (copy.containsKey(curchar)) {
                    copy.put(curchar, copy.get(curchar) + 1);
                }
            }
        }

        return result;

    }

    public boolean valid(HashMap<Character, Integer> map) {
        for (Map.Entry<Character, Integer> entry : map.entrySet()) {
            int value = entry.getValue();
            if (value > 0) {
                return true;
            }
        }
        return false;
    }
}
```
