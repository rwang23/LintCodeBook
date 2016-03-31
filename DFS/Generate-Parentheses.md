##Generate Parentheses

	Total Accepted: 83129 Total Submissions: 227840 Difficulty: Medium
	Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

	For example, given n = 3, a solution set is:

	"((()))", "(()())", "(())()", "()(())", "()()()"

####思路
- 典型DFS, 但是刚一开始并没想到如何如迭代
- 不要一来就想着优化,就直接想,罗列出所有组合,然后排除就行了
- 这个方法就是罗列所有,但是如果)的数量大于(就不符合要求

```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<String>();
        if (n <= 0) {
            return result;
        }
        dfs(result, new String(), 0, 0, n);
        return result;
    }

    public void dfs(List<String> result, String string, int left, int right, int n) {
        if (right > left) {
            return;
        }

        if (left == n && right == n) {
            result.add(new String(string));
            return;
        }

        if (left == n) {
            dfs(result, string + ")", left, right + 1, n);
            return;
        }

        dfs(result, string + "(", left + 1, right, n);
        dfs(result, string + ")", left, right + 1, n);
    }
}
```
