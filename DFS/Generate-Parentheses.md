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

####思路
- 从DP思路来思考
- Pair(n) 来源于 Pair(n - 1), 所以不断这么来源于底层
- O(n4)

```java
public class Solution
{
    public List<String> generateParenthesis(int n)
    {
        List<List<String>> lists = new ArrayList<>();
        lists.add(Collections.singletonList(""));

        for (int i = 1; i <= n; ++i)
        {
            final List<String> list = new ArrayList<>();

            for (int j = 0; j < i; ++j)
            {
                for (final String first : lists.get(j))
                {
                    for (final String second : lists.get(i - 1 - j))
                    {
                        list.add("(" + first + ")" + second);
                    }
                }
            }

            lists.add(list);
        }

        return lists.get(lists.size() - 1);
    }
}
```

####上边思路的DFS做法
```
For 2, it should place one "()" and add another one insert it but none tail it,

'(' f(1) ')' f(0)

or add none insert it but tail it by another one,

'(' f(0) ')' f(1)

Thus for n, we can insert f(i) and tail f(j) and i+j=n-1,

'(' f(i) ')' f(j)
```

```java
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<String>();
    if (n == 0) {
        result.add("");
    } else {
        for (int i = n - 1; i >= 0; i--) {
            List<String> insertSub = generateParenthesis(i);
            List<String> tailSub = generateParenthesis(n - 1 - i);
            for (String insert : insertSub) {
                for (String tail : tailSub) {
                    result.add("(" + insert + ")" + tail);
                }
            }

        }
    }
    return result;
}
```
