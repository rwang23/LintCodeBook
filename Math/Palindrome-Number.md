##Palindrome Number

Total Accepted: 116092 Total Submissions: 370028 Difficulty: Easy
Determine whether an integer is a palindrome. Do this without extra space.

####思路
- 直接做

```java
public class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }

        int temp = x;
        int base = 1;
        while (temp >= 10) {
            temp /= 10;
            base *= 10;
        }

        int firstNum = x;
        int lastNum = x;

        while (firstNum > 1) {
            int digit1 = firstNum / base;
            firstNum = firstNum % base;
            base /= 10;

            int digit2 = lastNum % 10;
            lastNum = lastNum / 10;

            if (digit1 != digit2) {
                return false;
            }
        }

        return true;
    }
}
```
