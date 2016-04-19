##Strobogrammatic Number II

	Total Accepted: 6692 Total Submissions: 20034 Difficulty: Medium
	A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

	Find all strobogrammatic numbers that are of length = n.

	For example,
	Given n = 2, return ["11","69","88","96"].

####思路
- DFS
- 自己写的coding style很不好,就不要参考了

```java
public class Solution {

    Map<Character, Character> map = new HashMap<Character, Character>();
    int[] nums = new int[]{0, 1, 8, 6, 9};
    public List<String> findStrobogrammatic(int n) {

        List<String> result = new ArrayList<String>();
        StringBuilder string = new StringBuilder();

        if (n == 1) {
            result.add("0");
            result.add("1");
            result.add("8");
            return result;
        }


        map.put('6', '9');
        map.put('9', '6');
        map.put('1', '1');
        map.put('0', '0');
        map.put('8', '8');



        dfs(result, string, n, 1);
        return result;
    }

    public void dfs(List<String> result, StringBuilder string, int n, int index) {
        StringBuilder sb = new StringBuilder(string);
        if (index - 1 == n / 2) {
            if (n % 2 == 0) {
                for (int i = sb.length() - 1; i >= 0; i--) {
                    char newChar = map.get(sb.charAt(i));
                    sb.append(newChar);
                }
                if (sb.length() == n && sb.charAt(0) != '0' ) {
                    result.add(new String(sb.toString()));
                }
            } else {
                for (int i = 0; i <= 2; i++) {
                    StringBuilder temp = new StringBuilder(sb);
                    temp.append(Integer.toString(nums[i]));
                    for (int k = temp.length() - 2; k >= 0; k--) {
                        char newChar = map.get(temp.charAt(k));
                        temp.append(newChar);
                    }
                    if (temp.length() == n && temp.charAt(0) != '0') {
                        result.add(new String(temp.toString()));
                    }
                }
            }
            return;
        }

        for (int i = index; i <= n / 2; i++) {
            for (int j = 0; j < nums.length; j++) {
                string.append(Integer.toString(nums[j]));
                dfs(result, string, n, i + 1);
                string.deleteCharAt(string.length() - 1);
            }
        }

    }
}
```

####更快的DFS
- 通过char array,避免了string的操作

```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        Map<Character, Character> map = new HashMap<Character, Character>();
        map.put('0', '0');
        map.put('1', '1');
        map.put('6', '9');
        map.put('8', '8');
        map.put('9', '6');
        List<String> result = new ArrayList<String>();
        char[] buffer = new char[n];
        dfs(n, 0, buffer, result, map);
        return result;
    }

    private void dfs(int n, int index, char[] buffer, List<String> result, Map<Character, Character> map) {
        if (n == 0) {
            return;
        }
        if (index == (n + 1) / 2) {
            result.add(String.valueOf(buffer));
            return;
        }
        for (Character c : map.keySet()) {
            if (index == 0 && n > 1 && c == '0') {  // first digit cannot be '0' when n > 1
                continue;
            }
            if (index == n / 2 && (c == '6' || c == '9')) {   // mid digit cannot be '6' or '9' when n is odd
                continue;
            }
            buffer[index] = c;
            buffer[n - 1 - index] = map.get(c);
            dfs(n, index + 1, buffer, result, map);
        }
    }
}
```

####一个简洁的办法

```java
public List<String> findStrobogrammatic(int n) {
    return helper(n, n);
}

List<String> helper(int n, int m) {
    if (n == 0) return new ArrayList<String>(Arrays.asList(""));
    if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));

    List<String> list = helper(n - 2, m);

    List<String> res = new ArrayList<String>();

    for (int i = 0; i < list.size(); i++) {
        String s = list.get(i);

        if (n != m) res.add("0" + s + "0");

        res.add("1" + s + "1");
        res.add("6" + s + "9");
        res.add("8" + s + "8");
        res.add("9" + s + "6");
    }

    return res;
}
```
