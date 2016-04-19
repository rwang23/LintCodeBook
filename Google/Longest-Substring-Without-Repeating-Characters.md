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

####暴力解法 O(n2)
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

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        Set<Character> set = new HashSet<Character>();
        char[] charArray = s.toCharArray();
        int size = s.length();

        int i = 0;
        int j = 0;
        int max = 0;

        while (j < size) {
            if (!set.contains(charArray[j])) {
                set.add(charArray[j++]);
                max = Math.max(max, j - i);
            } else {
                set.remove(charArray[i++]);
            }
        }

        return max;
    }
}

```

