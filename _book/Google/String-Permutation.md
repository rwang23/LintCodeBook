##String Permutation


	Given two strings, write a method to decide if one is a permutation of the other.

	Have you met this question in a real interview? Yes
	Example
	abcd is a permutation of bcad, but abbe is not a permutation of abe

####Tags Expand
String Permutation

####思路
- 利用hashmap 可以实现O(n)
- 或者利用排序, O(nlogn)

```java
public class Solution {
    /**
     * @param A a string
     * @param B a string
     * @return a boolean
     */
    public boolean stringPermutation(String A, String B) {
        // Write your code here
        if (A == null || B == null || A.length() != B.length()) {
            return false;
        }

        HashMap<Character, Integer> map = new HashMap<Character, Integer>();

        for (int i = 0; i < A.length(); i++) {
            char cur = A.charAt(i);
            if (map.containsKey(cur)) {
                map.put(cur, map.get(cur) + 1);
            } else {
                map.put(cur, 1);
            }
        }

        for (int i = 0; i < B.length(); i++) {
            char cur = B.charAt(i);
            if (map.containsKey(cur)) {
                map.put(cur, map.get(cur) - 1);
            } else {
                return false;
            }

            if (map.get(cur) == 0) {
                map.remove(cur);
            }
        }

        return map.size() == 0;
    }
}
```

####排序
```java
public boolean stringPermutation(String str1, String str2) {

    if (str1.length() != str2.length())
      return false;

    char[] a = str1.toCharArray();
    char[] b = str2.toCharArray();

    Arrays.sort(a);
    Arrays.sort(b);

    return Arrays.equals(a, b);
}
```
