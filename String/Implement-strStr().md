##Implement strStr()
[lintcode](https://www.lintcode.com/problem/implement-strstr/description)

	Total Accepted: 102097 Total Submissions: 412372 Difficulty: Easy
	Implement strStr().

	Returns the index of the first occurrence of target in source, or -1 if target is not part of source.

####思路
- 使用两个指针
- 这种问题一定要注意的是,第一个或者第二个指针的范围
- 这道题 第一个i指针 + target.length() 不可能比source.length()大,如果大了的话就没有符合的

```java
public class Solution {
    /*
     * @param source: source string to be scanned.
     * @param target: target string containing the sequence of characters to match
     * @return: a index to the first occurrence of target in source, or -1  if target is not part of source.
     */
    public int strStr(String source, String target) {
        // write your code here

        if (source == null || target == null) {
            return -1;
        }
        if (source.equals(target)) {
            return 0;
        }
        if (target.equals("")) {
            return 0;
        }
        if (source.equals("")) {
            return -1;
        }

        for (int i = 0; i + target.length() <= source.length(); i++) {
            for (int j = 0; j < target.length(); j++) {
                if (source.charAt(i + j) != target.charAt(j)) {
                    break;
                }
                if (j == target.length() - 1) {
                    return i;
                }
            }

        }
        return -1;
    }
}
```
