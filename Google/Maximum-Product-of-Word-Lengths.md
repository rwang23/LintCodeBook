##Maximum Product of Word Lengths

	Total Accepted: 16297 Total Submissions: 41606 Difficulty: Medium
	Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

	Example 1:
	Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]
	Return 16
	The two words can be "abcw", "xtfn".

	Example 2:
	Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]
	Return 4
	The two words can be "ab", "cd".

	Example 3:
	Given ["a", "aa", "aaa", "aaaa"]
	Return 0
	No such pair of words.

####思路
- brute force 直接强行比较两个字符串看是否有相同char,会比较慢
- 所以想到了,先用hashmap来存好每个字符串sort过后的char[] array,然后用两根指针来找是否有相同char
- 时间O(n2) 空间O(n)
- 不过还不是最好的解法,我们可以使用bit map来解决这道题

```java
public class Solution {
    public int maxProduct(String[] words) {
        if (words == null || words.length == 0) {
            return 0;
        }
        Map<String, char[]> map = new HashMap<String, char[]>();
        int n = words.length;
        int result = 0;
        for (int i = 0; i < n; i++) {
            String cur = words[i];
            char[] sortArray = cur.toCharArray();
            Arrays.sort(sortArray);
            map.put(cur, sortArray);
        }

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                String s1 = words[i];
                String s2 = words[j];
                if (shareSameChar(map.get(s1), map.get(s2))) {
                    continue;
                }
                result = Math.max(result, s1.length() * s2.length());
            }
        }
        return result;

    }

    public boolean shareSameChar(char[] array1, char[] array2) {
        int start1 = 0;
        int start2 = 0;
        while (start1 < array1.length && start2 < array2.length) {
            if (array1[start1] == array2[start2]) {
                return true;
            } else if (array1[start1] > array2[start2]) {
                start2++;
            } else {
                start1++;
            }
        }
        return false;
    }
}
```

####优化
- 因为题目中说都是小写字母，那么只有26位，一个整型数int有32位，我们可以用后26位来对应26个字母，若为1，说明该对应位置的字母出现过，那么每个单词的都可由一个int数字表示，两个单词没有共同字母的条件是这两个int数想与为0

```java
public class Solution {
    public int maxProduct(String[] words) {
        int n = words.length;
        int[] elements = new int[n];
        for (int i=0;i<n;i++){
            for(int j=0;j<words[i].length();j++){
                elements[i] |= 1 << (words[i].charAt(j) - 'a');
            }
        }

        int ans = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                if ((elements[i] & elements[j]) == 0)
                    ans = Math.max(ans,words[i].length() * words[j].length());
            }
        }
        return ans;
    }
}
```
