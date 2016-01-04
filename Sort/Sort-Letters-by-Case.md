##Sort Letters by Case

37% Accepted

	Given a string which contains only letters.
    Sort it by lower case first and upper case second.

	Have you met this question in a real interview? Yes
	Example
	For "abAcD", a reasonable answer is "acbAD"

####Note
It's not necessary to keep the original order of lower-case letters and upper case letters.

####Challenge
Do it in one-pass and in-place.

####Tags Expand
String Two Pointers LintCode Copyright Sort

```java
public class Solution {
    /**
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] chars) {
        if (chars == null || chars.length == 0) {
            return;
        }
        char pivot = 'a';
        int start = 0; int end = chars.length - 1;
        while (start <= end) {
            while (start <= end && chars[start] >= pivot) {
                start++;
            }
            while (start <= end && chars[end] < pivot) {
                end--;
            }
            if (start <= end) {
                char temp = chars[end];
                chars[end] = chars[start];
                chars[start] = temp;
                start++;
                end--;
            }
        }
    }
}


```

####Comparator的方法
```java
public class Solution {
    /**
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] input) {
        //write your code here
        Character[] temp = new Character[input.length];
        for (int i = 0; i < input.length; i++) {
            temp[i] = input[i];
        }
        //Arrays.sort(temp, new letterComparator<Character>());
        Arrays.sort(temp, new Comparator<Character>() {
            public int compare(Character c1, Character c2) {
            int i1 = c1 >= 'a' ? (int)c1 - 'a' : (int)c1;
            int i2 = c2 >= 'a' ? (int)c2 - 'a' : (int)c2;
            return i1 - i2;
            }
        });
        for (int i = 0; i < input.length; i++) {
            input[i] = temp[i];
        }
    }

}

```
####Comparator方法
```java
public class Solution {
    /**
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] input) {
        //write your code here
        Character[] temp = new Character[input.length];
        for (int i = 0; i < input.length; i++) {
            temp[i] = input[i];
        }
        //Arrays.sort(temp, new letterComparator<Character>());
        Arrays.sort(temp, new letterComparator());
        for (int i = 0; i < input.length; i++) {
            input[i] = temp[i];
        }
    }

    public class letterComparator implements Comparator<Character> {
        public int compare(Character c1, Character c2) {
            int i1 = c1 >= 'a' ? (int)c1 - 'a' : (int)c1;
            int i2 = c2 >= 'a' ? (int)c2 - 'a' : (int)c2;
            return i1 - i2;
        }
    }
}

```
