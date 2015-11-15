##Longest Substring Without Repeating Characters

26% Accepted
	Given a string, find the length of the longest substring without repeating characters.

	Example
	For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3.

	For "bbbbb" the longest substring is "b", with the length of 1.

####Challenge
-O(n) time

####Tags Expand
- String
- Two Pointers
- Hash Table

####暴力解法 O(n)
```java
public class Solution {
    /**
     * @param s: a string
     * @return: an integer
     */
    public int lengthOfLongestSubstring(String s) {
        // write your code here
        if (s == "" || s == null || s.length() == 0) {
            return 0;
        }
        int size = s.length();
        int max = Integer.MIN_VALUE;

        for (int i = 0; i < size; i++) {
            HashSet<Character> hashset = new HashSet<Character>();
            int count = 0;
            for (int j = i; j < size; j++) {
                if (!hashset.contains(s.charAt(j))) {
                    hashset.add(s.charAt(j));
                    count++;
                } else {
                    break;
                }
                max = Math.max(max, count);

            }
        }

        return max;
    }
}

```

####优化解法 O(n)
- 假设[0,3]最长,那么不用去找[1,3] [2,3], 所以i++的时候 j不一定需要变
- 去找的时候[1, ?] j++ 去找[1,4]
- 注意边界条件 i==0的时候,没有remove这些操作,而且i!=0时候,remove的也是charAt(i-1)

```java
public class Solution {
    /**
     * @param s: a string
     * @return: an integer
     */
    public int lengthOfLongestSubstring(String s) {
        // write your code here
        if (s == "" || s == null || s.length() == 0) {
            return 0;
        }

        HashSet<Character> hashset = new HashSet<Character>();
        int size = s.length();
        int max = Integer.MIN_VALUE;
        int count = 0;

        for (int i = 0, j = 0; i < size && j <= size; i++) {

            if (i != 0 && hashset.contains(s.charAt(i -1))) {
                hashset.remove(s.charAt(i -1));
                count--;
            }

            while (j < size && !hashset.contains(s.charAt(j))) {
                count++;
                hashset.add(s.charAt(j));
                j++;
            }

            max = Math.max(max, count);
        }

        return max;
    }
}

```


####优化解法
- 把 char key = target.charAt(k) 单独写出来,否则 hashmap.containsKey(target.charAt(k)), 特别是些hashmap.put的时候太容易出低级bug
- [0,6] --> 不需要找[0,7], 去找[1,6],如果[1,6]不行,再[1,7]
- 这样的两根指针优化,常常用在,可以直接想到i,j两重循环去做,然后去思考是不是可以忽略一些情况,就变成两根指针同时前进,优化少掉一层负责度数量级

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
            char key = target.charAt(k);
            if (!hashmap.containsKey(key)) {
                hashmap.put(key, 1);
            } else {
                hashmap.put(key, hashmap.get(key) + 1);
            }
        }

        int count = 0;
        for (int i = 0, j = 0; i < size && j <= size; i++) {
            if (i != 0 && hashmap.containsKey(source.charAt(i - 1))) {
                char key = source.charAt(i - 1);
                hashmap.put(key, hashmap.get(key) + 1);
                count--;
            }

            while (j < size && !isValid(hashmap, target)) {
                char key = source.charAt(j);
                if (hashmap.containsKey(key)) {
                    hashmap.put(key, hashmap.get(key) - 1);
                }
                count++;
                j++;
            }

            if (isValid(hashmap, target)) {
                min = Math.min(min, count);
                if (min == count) {
                    result = source.substring(i, j);
                }
            }

        }
        return result;
    }

    public boolean isValid(HashMap<Character, Integer> hashmap, String target) {
        boolean valid = true;
        for (int i = 0; i < target.length(); i++) {
            char key = target.charAt(i);
            if (!hashmap.containsKey(key)) {
                valid = false;
                break;
            }
            if (hashmap.get(key) > 0 ) {
                valid = false;
                break;
            }
        }
        return valid;
    }
}

```
