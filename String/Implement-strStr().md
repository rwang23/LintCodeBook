##Implement strStr()

	Total Accepted: 102097 Total Submissions: 412372 Difficulty: Easy
	Implement strStr().

	Returns the index of the first occurrence of target in source, or -1 if target is not part of source.

####思路
- 两个for loop需要n3
- 两个指针问题

```java
public class Solution {
    public int strStr(String source, String target) {
        if (source == null && target == null) {
            return -1;
        }
        if (source == null || target == null || source.length() < target.length()) {
            return -1;
        }

        int m = source.length();
        int n = target.length();
        int sourcePrePointer = 0;
        while (sourcePrePointer + n <= m) {
            int sourceCurPointer = sourcePrePointer;
            int targetPointer = 0;
            while (targetPointer < n && sourceCurPointer < m &&  source.charAt(sourceCurPointer) == target.charAt(targetPointer)) {
                sourceCurPointer++;
                targetPointer++;
            }

            if (targetPointer == n) {
                return sourcePrePointer;
            } else {
                sourcePrePointer++;
            }
        }

        return -1;
    }
}
```
