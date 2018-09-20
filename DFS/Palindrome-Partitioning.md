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

###先生成palindrome的数组，到时候判断不用再去计算一次，省时间
- 注意生成palindrom的数组的时候的动态规划
- state： f[i][j] i到j的substring是不是palindrome
- fcuntion:  f[i][j] = f[i+1][j-1] && char(i) == char(j)
- initial: f[i][i] = true, f[i][i + 1] = char(i) == char(i + 1)
- answer: f[i][j]
-  注意下面的顺序，先每次+2地走进行遍历，再+3走进行遍历，而不是先开始遍历，再+2，+3
```java
	 for (int len = 2; len < size; len++) {
         	for (int i = 0; i + len < size; i++) 
```
##解法
```java
public class Solution {
    /*
     * @param s: A string
     * @return: A list of lists of string
     */
    public List<List<String>> partition(String s) {
        // write your code here
        List<List<String>> results = new ArrayList<List<String>>();
        List<String> result = new ArrayList<String>();
        if (s == null || s.equals("")) {
            results.add(result);
            return results;
        }
        
        boolean[][] isPalindrome = buildMap(s);
        dfs(results, result, isPalindrome, s, 0);
        
        return results;
        
        
    }
    
    public void dfs(List<List<String>> results, List<String> result, boolean[][] isPalindrome, String string, int index) {
        
        if (index == string.length()) {
            List<String> cur = new ArrayList<String>(result);
            results.add(cur);
            return;
        }
        
        for (int len = 1; len + index <= string.length(); len++) {
            if (isPalindrome[index][index + len - 1]) {
                String curString = string.substring(index, index + len); 
                result.add(curString);
                dfs(results, result, isPalindrome, string, index + len);
                result.remove(result.size() - 1);
            }
        }
        
    }
    
    public boolean[][] buildMap(String string) {
        int size = string.length();
        boolean[][] isPalindrome = new boolean[size][size];
        
        for (int i = 0; i < size; i++) {
            if (i + 1 < size) {
                isPalindrome[i][i + 1] = (string.charAt(i) == string.charAt(i + 1));
            }
            isPalindrome[i][i] = true;
        }
        
        for (int len = 2; len < size; len++) {
            for (int i = 0; i + len < size; i++) {
                int j = i + len;
                isPalindrome[i][j] = isPalindrome[i + 1][j - 1] && (string.charAt(i) == string.charAt(j));
                
            }
        }

        return isPalindrome;
    }
}
```
