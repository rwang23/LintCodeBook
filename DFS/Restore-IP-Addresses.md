##Restore IP Addresses
	Total Accepted: 52655 Total Submissions: 228619 Difficulty: Medium
	Given a string containing only digits, restore it by returning all possible valid IP address combinations.

	For example:
	Given "25525511135",

	return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

####思路
- 这道题一看就是DFS,但是没想清楚怎么去写更好直接写DFS就会造成混乱,思考好了再写
- 有效的IP 每一部分, 必须在[0,255]之间,并且不能出现01 011,就是二位三位长,但是首位为0
- 最开始写的时候,乱成了浆糊
- 后来改了改,没有直接输出string加入到result,而是分别把每个部分先求出来,这样就容易了很多

```java
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> result = new ArrayList<String>();
        if (s == null || s.length() < 4 || s.length() > 12) {
            return result;
        }

        List<String> list = new ArrayList<String>();
        dfs(result, list, 0, s);
        return result;
    }

    public void dfs(List<String> result, List<String> list, int start, String s) {
        if (list.size() == 4) {
            if (start == s.length()) {
                String validString = list.get(0) + "." + list.get(1) + "." + list.get(2) + "." + list.get(3);
                result.add(validString);
            } else {
                return;
            }
        }

        for (int i = start; i <= start + 3 && i < s.length(); i++) {
            String temp = s.substring(start, i + 1);
            if (isValid(temp)) {
                list.add(temp);
                dfs(result, list, i + 1, s);
                list.remove(list.size() - 1);
            }
        }
    }

    public boolean isValid(String s) {
        if (s == null || s.length() == 0) {
            return false;
        }x
        if (s.length() >= 2 && s.charAt(0) == '0') {
            return false;
        }
        int digit = Integer.valueOf(s);
        if (digit > 255 || digit < 0) {
            return false;
        }
        return true;
    }
}
```
