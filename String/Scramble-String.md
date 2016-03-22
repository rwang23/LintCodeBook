##Scramble String
    Total Accepted: 43919 Total Submissions: 167323 Difficulty: Hard
    Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

    Below is one possible representation of s1 = "great":

        great
       /    \
      gr    eat
     / \    /  \
    g   r  e   at
               / \
              a   t
    To scramble the string, we may choose any non-leaf node and swap its two children.

    For example, if we choose the node "gr" and swap its two children, it produces a scrambled string "rgeat".

        rgeat
       /    \
      rg    eat
     / \    /  \
    r   g  e   at
               / \
              a   t
    We say that "rgeat" is a scrambled string of "great".

    Similarly, if we continue to swap the children of nodes "eat" and "at", it produces a scrambled string "rgtae".

        rgtae
       /    \
      rg    tae
     / \    /  \
    r   g  ta  e
           / \
          t   a
    We say that "rgtae" is a scrambled string of "great".

    Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.


####思路

####朴素暴力递归解法
- 跟二叉树层类似,层层递归即可
- lintcode能通过 leetcode不能

```java
public class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1 == null && s2 == null) {
            return true;
        }

        if (s1 == null || s2 == null || s1.length() != s2.length()) {
            return false;
        }

        if (s1.equals(s2)) {
            return true;
        }

        for (int i = 0; i < s1.length() - 1; i++) {
            String s11 = s1.substring(0, i + 1);
            String s12 = s1.substring(i + 1, s1.length());

            String s21 = s2.substring(0, i + 1);
            String s22 = s2.substring(i + 1, s2.length());

            String s23 = s2.substring(s2.length() - i - 1, s2.length());
            String s24 = s2.substring(0, s2.length() - i - 1);

            if ((isScramble(s11, s21) && isScramble(s12, s22)) || (isScramble(s11, s23) && isScramble(s12, s24))) {
                return true;
            }
        }

        return false;
    }
}

```
####剪枝优化
- 增加了判断条件
- 如果本来字符就不同,那就不满足,就return false,很大地提高了速度,可通过leetcode

```java
public class Solution {
    public boolean isScramble(String s1, String s2) {
        if (s1 == null && s2 == null) {
            return true;
        }

        if (s1 == null || s2 == null || s1.length() != s2.length()) {
            return false;
        }

        char[] s1Char = s1.toCharArray();
        char[] s2Char = s2.toCharArray();
        Arrays.sort(s1Char);
        Arrays.sort(s2Char);
        String new1 = new String(s1Char);
        String new2 = new String(s2Char);

        if (!new1.equals(new2)) {
            return false;
        }

        if (s1.equals(s2)) {
            return true;
        }

        for (int i = 0; i < s1.length() - 1; i++) {
            String s11 = s1.substring(0, i + 1);
            String s12 = s1.substring(i + 1, s1.length());

            String s21 = s2.substring(0, i + 1);
            String s22 = s2.substring(i + 1, s2.length());

            String s23 = s2.substring(s2.length() - i - 1, s2.length());
            String s24 = s2.substring(0, s2.length() - i - 1);

            if ((isScramble(s11, s21) && isScramble(s12, s22)) || (isScramble(s11, s23) && isScramble(s12, s24))) {
                return true;
            }
        }

        return false;
    }
}

```


####Memorization优化
- 写了hashmap作为memorization的优化但是没完全通过,debug了好一阵,直接引用[参考资料](https://shanzi.gitbooks.io/algorithm-notes/content/problem_solutions/scramble_string.html)吧
- 这个key直接用的是s1 + " " + s2, value就是true or false
- hashmap最方便,否则要使用三维数组
- 使用三维数组的话:index1记忆S1起始地址，index2记忆S2起始地址，len 表示字符串的长度。这样我们可以用一个三维数组来记录计算过的值
- 这个三维数组一个是N^3的复杂度，在每一个递归中，要从1-len地计算一次所有的子串，所以一共的复杂度是N^4

```java
public class Solution {
    private boolean isScramble(String s1, String s2, Map<String, Boolean> cache) {

        if (s1.equals(s2)) return true;
        if (s1.length() <= 1) return false;
        String cacheKey = s1 + " " + s2;
        if (cache.containsKey(cacheKey)) return cache.get(cacheKey);

        boolean flag = false;
        int n = s1.length();
        for (int i = 1; i < n; i++) {
            if (isScramble(s1.substring(0, i), s2.substring(0, i), cache)
                && isScramble(s1.substring(i), s2.substring(i), cache)) {
                    flag = true;
                    break;
                }

            if (isScramble(s1.substring(0, i), s2.substring(n - i, n), cache)
                && isScramble(s1.substring(i, n), s2.substring(0, n - i), cache)) {
                    flag = true;
                    break;
                }
        }

        cache.put(cacheKey, flag);
        return flag;
    }

    public boolean isScramble(String s1, String s2) {
        if (s1.isEmpty() && s2.isEmpty()) return true;

        HashMap<String, Boolean> cache = new HashMap<String, Boolean>();
        return isScramble(s1, s2, cache);
    }
}
```

####还有动规解法
- [参考](http://www.cnblogs.com/TenosDoIt/p/3452004.html)
