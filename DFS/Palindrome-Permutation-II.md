##Palindrome Permutation II
	Total Accepted: 5002 Total Submissions: 18130 Difficulty: Medium
	Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

	For example:

	Given s = "aabb", return ["abba", "baab"].

	Given s = "abc", return [].

####思路
- 类似与PermutationII的做法和优化,超时
- 应该只需要取一半String来做就可以了

```java
public class Solution {

    public boolean canPermutePalindrome(String s) {
        Set<Character> set=new HashSet<Character>();
        for(int i = 0; i < s.length(); ++i){
            if (!set.contains(s.charAt(i))) {
                set.add(s.charAt(i));
            }
            else {
                set.remove(s.charAt(i));
            }
        }
        return set.size()==0 || set.size()==1;
    }

    public List<String> generatePalindromes(String s) {
        List<String> result = new ArrayList<>();
        if (s == null || !canPermutePalindrome(s)) {
            return result;
        }

        char[] array = s.toCharArray();
        Arrays.sort(array);

        StringBuilder sb = new StringBuilder();
        Set<Integer> set = new HashSet<Integer>();
        dfs(result, array, set, sb);

        return result;
    }

    public void dfs(List<String> result, char[] array, Set<Integer> set, StringBuilder sb) {
        if (sb.length() == array.length) {
            if (isPalindrome(sb.toString())) {
                result.add(new String(sb.toString()));
            }
            return;
        }

        for (int i = 0; i < array.length; i++) {
            char cur = array[i];
            if (set.contains(i)) {
                continue;
            }
            if (i != 0 && array[i] == array[i - 1] && !set.contains(i - 1)) {
                continue;
            }

            sb.append(cur);
            set.add(i);
            dfs(result, array, set, sb);
            sb.setLength(sb.length() - 1);
            set.remove(i);
        }
    }

    public boolean isPalindrome(String s) {
        if (s == null) {
            return true;
        }

        int size = s.length();
        int start = 0;
        int end = size - 1;
        while (start < end) {
            char schar = s.charAt(start);
            char echar = s.charAt(end);
            if (schar != echar) {
                return false;
            }
            start++;
            end--;
        }

        return true;
    }
}
```

####优化
- 去一半字符串来进行处理
- 值得注意的情况是,中间有可能是单个的字符,要单个考虑

```java
public class Solution {

    public boolean canPermutePalindrome(String s) {
        Set<Character> set = new HashSet<Character>();
        for(int i = 0; i < s.length(); i++){
            if (!set.contains(s.charAt(i))) {
                set.add(s.charAt(i));
            }
            else {
                set.remove(s.charAt(i));
            }
        }
        return set.size() == 0 || set.size() == 1;
    }

    public List<String> generatePalindromes(String s) {
        List<String> result = new ArrayList<>();
        if (s == null || !canPermutePalindrome(s)) {
            return result;
        }

        char[] array = s.toCharArray();
        Arrays.sort(array);
        List<Character> list = new ArrayList<>();
        char singleChar = ' ';
        for (int i = 0; i < array.length;) {
            if (i < array.length - 1 && array[i] == array[i + 1]) {
                list.add(array[i]);
                i += 2;
                continue;
            }
            singleChar = array[i];
            i++;
        }

        StringBuilder sb = new StringBuilder();
        Set<Integer> set = new HashSet<Integer>();
        dfs(result, list, set, sb, singleChar);

        return result;
    }

    public void dfs(List<String> result, List<Character> list, Set<Integer> set, StringBuilder sb, char singleChar) {
        if (sb.length() == list.size()) {
            int size = sb.length();
            if (singleChar != ' ') {
                sb.append(singleChar);
            }

            for (int i = size - 1; i >= 0; i--) {
                sb.append(sb.charAt(i));
            }
            result.add(new String(sb.toString()));
            return;
        }

        for (int i = 0; i < list.size(); i++) {
            char cur = list.get(i);
            if (set.contains(i)) {
                continue;
            }
            if (i != 0 && list.get(i) == list.get(i - 1) && !set.contains(i - 1)) {
                continue;
            }

            int size = sb.length();
            sb.append(cur);
            set.add(i);
            dfs(result, list, set, sb, singleChar);
            sb.setLength(size);
            set.remove(i);
        }
    }
}
```
