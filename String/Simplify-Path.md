##Simplify Path

	Total Accepted: 49930 Total Submissions: 228873 Difficulty: Medium
	Given an absolute path for a file (Unix-style), simplify it.

	For example,
	path = "/home/", => "/home"
	path = "/a/./b/../../c/", => "/c"
	click to show corner cases.

	Corner Cases:
	Did you consider the case where path = "/../"?
	In this case, you should return "/".
	Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
	In this case, you should ignore redundant slashes and return "/home/foo".

####思路
- 用一个stack存之前的dir,当遇到..时pop
- 这个题不难,但是debug花了很久时间,最后发现是,自己判断空的substring的时候,用的是 str == null
- 但是其实应该用str.equals(""),空是"",而不是null

```java
/*
if new dir then save into stack
if .. then pop it out
if . ignore
when return, should add slash before the dir
if stack empty then return /
if two slash, continue
*/


public class Solution {
    public String simplifyPath(String path) {
        if (path == null || path.length() == 0) {
            return new String();
        }

        int size = path.length();
        Stack<String> stack = new Stack<String>();
        int i = 0;
        while (i < size) {
            int j = i + 1;
            while (j < size && path.charAt(j) != '/') {
                j++;
            }
            String dir = path.substring(i + 1, j);
            i = j;
            if (dir.equals("") || dir.equals("/") || dir.equals(".")) {
                continue;
            } else if (dir.equals("..")) {
                if (!stack.isEmpty()) {
                    stack.pop();
                }
            } else {
                stack.push(dir);
            }
        }

        List<String> list = new ArrayList<String>();
        if (stack.isEmpty()) {
            return new String("/");
        }

        while (!stack.isEmpty()) {
            list.add(stack.pop());
        }
        StringBuilder sb = new StringBuilder();

        for (i = list.size() - 1; i >= 0; i--) {
            sb.append("/");
            sb.append(list.get(i));
        }
        return sb.toString();
    }
}
```
