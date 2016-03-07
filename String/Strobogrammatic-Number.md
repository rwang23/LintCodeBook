##Strobogrammatic Number

	Total Accepted: 7729 Total Submissions: 21559 Difficulty: Easy
	A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

	Write a function to determine if a number is strobogrammatic. The number is represented as a string.

	For example, the numbers "69", "88", and "818" are all strobogrammatic.

####思路
- HashMap

```java
public class Solution {
    public boolean isStrobogrammatic(String num) {
        if (num == null) {
            return true;
        }

        Map<Character, Character> map = new HashMap<Character, Character>();
        map.put('6', '9');
        map.put('9', '6');
        map.put('1', '1');
        map.put('0', '0');
        map.put('8', '8');

        for (int i = 0, j = num.length() - 1; i <= j; i++, j--) {
            if (!map.containsKey(num.charAt(i)) || !map.containsKey(num.charAt(j))) {
                return false;
            }

            if (num.charAt(i) == map.get(num.charAt(j))) {
                continue;
            } else {
                return false;
            }
        }

        return true;
    }
}
```
