##Reverse Words in a String

	Total Accepted: 93637 Total Submissions: 599510 Difficulty: Medium
	Given an input string, reverse the string word by word.

	For example,
	Given s = "the sky is blue",
	return "blue is sky the".

####思路
- 题目其实很简单,但是一定要用test case去验证,
- 很多小边界条件容易出错, 比如输入时 " 1"
- 这个时候split会得到两个值,一个是"",另一个是"1"


```java
public class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }

        String[] list = s.split(" ");
        StringBuilder sb = new StringBuilder();

        for (int i = list.length - 1; i >= 0; i--) {
            if (list[i].equals("")) continue;
            if (i != list.length - 1) {
                sb.append(" ");
            }
            sb.append(list[i]);
        }
        return sb.toString();
    }
}
```

####Built in function

```java
public String reverseWords(String s) {
    String[] words = s.trim().split(" +");
    Collections.reverse(Arrays.asList(words));
    return String.join(" ", words);
}
```
