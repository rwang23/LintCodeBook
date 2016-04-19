##Bulls and Cows

	Total Accepted: 24403 Total Submissions: 83555 Difficulty: Easy
	You are playing the following Bulls and Cows game with your friend:
	You write down a number and ask your friend to guess what the number is.
	Each time your friend makes a guess, you provide a hint that indicates how many digits in said
	 guess match your secret number exactly in both digit and position (called "bulls")
	 and how many digits match the secret number but locate in the wrong position (called "cows").
	 Your friend will use successive guesses and hints to eventually derive the secret number.

	For example:

	Secret number:  "1807"
	Friend's guess: "7810"
	Hint: 1 bull and 3 cows.
	(The bull is 8, the cows are 0, 1 and 7.)
	Write a function to return a hint according to the secret number and friend's guess,
	use A to indicate the bulls and B to indicate the cows.
	In the above example, your function should return "1A3B".

	Please note that both secret number and friend's guess may contain duplicate digits, for example:

	Secret number:  "1123"
	Friend's guess: "0111"
	In this case, the 1st 1 in friend's guess is a bull,
	the 2nd or 3rd 1 is a cow, and your function should return "1A1B".
	You may assume that the secret number and your friend's guess only contain digits,
	and their lengths are always equal.

####思路
- 用一个hashmap(或者一个int[10]数组就可以,只有10位)
- 我这个解法没有看到their lengths are always equal 这句话
- 不然可以减少一个loop

```java
public class Solution {
    public String getHint(String secret, String guess) {
        if (secret == null || secret.length() == 0) {
            return new String();
        }

        int bulls = 0;
        int cows = 0;
        int size1 = secret.length();
        int size2 = guess.length();
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        int i = 0;
        for (i = 0; i < Math.min(size1, size2); i++) {
            char s = secret.charAt(i);
            char g = guess.charAt(i);
            if (s == g) {
                bulls++;
            }
            if (map.containsKey(s)) {
                map.put(s, map.get(s) + 1);
            } else {
                map.put(s, 1);
            }

        }

        for (; i < size1; i++) {
            char s = secret.charAt(i);
            if (map.containsKey(s)) {
                    map.put(s, map.get(s) + 1);
                } else {
                    map.put(s, 1);
            }
        }

        for (i = 0; i < size2; i++) {
            char g = guess.charAt(i);
            if (map.containsKey(g)) {
                cows++;
                map.put(g, map.get(g) - 1);
                if (map.get(g) == 0) {
                    map.remove(g);
                }
            }
        }

        cows = cows - bulls;
        StringBuilder string = new StringBuilder();
        string.append(bulls);
        string.append('A');
        string.append(cows);
        string.append('B');
        return string.toString();
    }
}
```

####One pass solution
[leetcode](https://leetcode.com/discuss/67031/one-pass-java-solution)
