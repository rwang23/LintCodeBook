##Palindrome Permutation

	Total Accepted: 11227 Total Submissions: 22276 Difficulty: Easy
	Given a string, determine if a permutation of the string could form a palindrome.

	For example,
	"code" -> False, "aab" -> True, "carerac" -> True.

####思路
- Sort: Time: O(nlogn) Space 0(1)
- HashSet: Time: O(n) Spcace O(n)

####Sort
```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        if (s == null || s.length() == 0) {
            return true;
        }

        int size = s.length();
        char[] array = s.toCharArray();
        Arrays.sort(array);

        if (size % 2 == 0) {
            for (int i = 0; i + 1< size; i = i + 2) {
                if (array[i] != array[i + 1]) {
                    return false;
                }
            }
        } else {
            boolean singleCharAlready = false;
            for (int i = 0; i + 1 < size;) {
                if (array[i] != array[i + 1]) {
                    if (singleCharAlready) {
                        return false;
                    }
                    singleCharAlready = true;
                    i++;
                    continue;
                }
                i = i + 2;
            }
        }

        return true;
    }
}
```

####HashSet
```java
public class Solution {
    public boolean canPermutePalindrome(String s) {
        Set<Character> set=new HashSet<Character>();
        for(int i=0; i<s.length(); ++i){
            if (!set.contains(s.charAt(i)))
                set.add(s.charAt(i));
            else
                set.remove(s.charAt(i));
        }
        return set.size()==0 || set.size()==1;
    }
}
```
