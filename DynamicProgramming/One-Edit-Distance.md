##One Edit Distance

	Total Accepted: 11483 Total Submissions: 40581 Difficulty: Medium
	Given two strings S and T, determine if they are both one edit distance apart.

####思路
- 简化版的edit distance
- 这个只需要求满足是否为1
- 两个指针分别先指向最后一个字符,然后比较,如果相等,则i--,j--,如果不等,则把较长的那个的指针--再比较(因为如果只有一个distance,去掉了之后肯定就是完全一样了)
- 同时要注意,如果当i==0 或者j==0的时候,就distance就加上另外一边

```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        if (s == null && t == null) {
            return false;
        }
        if (s == null || s.length() == 0) {
            return t.length() == 1;
        }
        if (t == null || t.length() == 0) {
            return s.length() == 1;
        }

        int m = s.length();
        int n = t.length();

        int i = m;
        int j = n;
        int distance = 0;
        while (i >= 0 && j >= 0) {

            if (i == 0) {
                distance += j;
                break;
            }
            if (j == 0) {
                distance += i;
                break;
            }

            char c1 = s.charAt(i - 1);
            char c2 = t.charAt(j - 1);

            if (c1 == c2) {
                i--;
                j--;
            } else {
                if (m == n) {
                    i--;
                    j--;
                } else {
                    int maxLen = Math.max(m, n);
                    if (maxLen == m) {
                        i--;
                    } else {
                        j--;
                    }
                }
                distance++;
            }

            if (distance > 1) {
                return false;
            }
        }

        return distance == 1;
    }
}
```

####写起来简单一点
```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
      if (s == null || t == null)
        return false;

      if (s.length() > t.length())
        return isOneEditDistance(t, s);

      int i = 0, j = 0;

      while (i < s.length() && j < t.length()) {
        if (s.charAt(i) != t.charAt(j)) {
          // we try to replace s[i] with s[j] or insert s[j] to s[i]
          // then compare the rest and see if they are the same
          return s.substring(i + 1).equals(t.substring(j + 1)) ||
                 s.substring(i).equals(t.substring(j + 1));
        }

        i++; j++;
      }

      return t.length() - j == 1;
    }
}
```
