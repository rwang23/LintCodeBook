##Reverse Vowels of a String
	Total Accepted: 2932 Total Submissions: 7986 Difficulty: Easy
	Write a function that takes a string as input and reverse only the vowels of a string.

	Example 1:
	Given s = "hello", return "holle".

	Example 2:
	Given s = "leetcode", return "leotcede".

```java
public class Solution {
    public String reverseVowels(String s) {
        if (s == null || s.equals("")) {
            return new String();
        }
        int start = 0;
        int end = s.length() - 1;
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('e');
        set.add('i');
        set.add('o');
        set.add('u');
        set.add('A');
        set.add('E');
        set.add('I');
        set.add('O');
        set.add('U');
        char[] array = s.toCharArray();


        while (start < end) {

            while (start < end && !set.contains(array[start])) {
                start++;
            }

            while (start < end && !set.contains(array[end])) {
                end--;
            }

            if (start < end) {
                swap(array, start, end);
                start++;
                end--;
            }
        }

        return new String(array);
    }

    public void swap(char[] array, int index1, int index2) {
        char temp = array[index1];
        array[index1] = array[index2];
        array[index2] = temp;
    }
}
```
