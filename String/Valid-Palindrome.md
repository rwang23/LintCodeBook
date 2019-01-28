##Valid Palindrome
	Difficulty: Easy
	Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

	For example,
	"A man, a plan, a canal: Panama" is a palindrome.
	"race a car" is not a palindrome.

	Note:
	Have you consider that the string might be empty? This is a good question to ask during an interview.

	For the purpose of this problem, we define empty string as valid palindrome.

####思路
- 用了regular expression 提出去string array然后合并成string再判断,超时了
- 所以就直接做了(可以用两个指针,也可以用stack类似于判断括号是否一致的办法)
- 这个方法不是很好,不需要用hashset
- 可以写一个valid character函数来判断是不是有效就可以,
- 比如

```java
public boolean isValid(char c)
{
    return (c >= 'a' && c <= 'z' || c >= 'A' && c <= 'Z' || c >= '0' && c <= '9') ? true : false;
}
```
- 也可以这么做

```java
s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();
```

####代码
```java
public class Solution {
    /**
     * @param s: A string
     * @return: Whether the string is a valid palindrome
     */
    public boolean isPalindrome(String s) {
        // write your code here
        if (s.equals("")) {
            return true;
        }

        for (int i = 0, j = s.length() - 1; i < j; i++, j--) {
            char c1 = s.charAt(i);
            char c2 = s.charAt(j);

            while (i < j && !Character.isLetterOrDigit(c1)) {
                i++;
                c1 = s.charAt(i);
            }

            while (i < j && !Character.isLetterOrDigit(c2)) {
                j--;
                c2 = s.charAt(j);
            }

            if (Character.toUpperCase(c1) != Character.toUpperCase(c2)) {
                return false;
            }
        }

        return true;
    }
}
```
