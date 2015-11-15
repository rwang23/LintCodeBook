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
