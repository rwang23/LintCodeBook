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

