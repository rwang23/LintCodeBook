##Palindrome Partitioning

22% Accepted

	Given a string s, partition s such that every substring of the partition is a palindrome.

	Return all possible palindrome partitioning of s.

	Have you met this question in a real interview? Yes
	Example
	Given s = "aab", return:

	[
	  ["aa","b"],
	  ["a","a","b"]
	]

####Tags Expand
- Backtracking
- Depth First Search

####思路
- 求所有答案，标准DFS题
- 这个题有很多值得注意的地方，见注释
- 最值得注意的地方就是pos的传入,
- 要先画图画清楚,Pos是如何作用的

```java
public class Solution {
    /**
     * @param s: A string
     * @return: A list of lists of string
     */

    public List<List<String>> partition(String s) {
         List<List<String>> result = new ArrayList<List<String>>();
        if (s == null) {
            return result;
        }
        //不能List<String> list = new ArrayList<String>() 因为List是abstract类型
        List<String> list = new ArrayList<String>();
        partitionhelper(s, 0, list, result);
        return result;
    }

    public void partitionhelper(String s, int pos, List<String> list, List<List<String>> result) {
        if (pos == s.length()) {
        	//一定是new ArrayList<String>(list)，否则的话，就把原来list的地址跟result连起来了，如果list改变，那么result里边的内容也改变了
            result.add(new ArrayList<String>(list));
            return;
        }
        for (int i = pos + 1; i <= s.length(); i++) {
            String string = s.substring(pos, i);
            if (!isPalindrome(string)) {
                continue;
            }
            list.add(string);
            partitionhelper(s, i, list, result);
            list.remove(list.size() - 1);
        }
    }

    public boolean isPalindrome(String s) {
        int beg = 0;
        int end = s.length() - 1;
        //不必要去设置i++ j-- 多麻烦，一个while就搞定
        while (beg < end) {
            if (s.charAt(beg) != s.charAt(end)) {
                return false;
            }
            beg++;
            end--;
        }
        return true;
    }
}

```

