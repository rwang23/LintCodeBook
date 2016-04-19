##Happy Number

	Write an algorithm to determine if a number is happy.

	A happy number is a number defined by the following process:
	Starting with any positive integer, replace the number by the sum of the squares of its digits,
	and repeat the process until the number equals 1 (where it will stay),
	or it loops endlessly in a cycle which does not include 1.
	Those numbers for which this process ends in 1 are happy numbers.

	Have you met this question in a real interview? Yes
	Example
	19 is a happy number

	1^2 + 9^2 = 82
	8^2 + 2^2 = 68
	6^2 + 8^2 = 100
	1^2 + 0^2 + 0^2 = 1

####Tags Expand
Hash Table Mathematics


####思路
- 考察的就是求位数上的数字
- 用hashset保存之前生成的值

```java
public class Solution {
    /**
     * @param n an integer
     * @return true if this is a happy number or false
     */
    public boolean isHappy(int n) {
        // Write your code here
        if (n <= 0) {
            return false;
        }

        int sum = 0;
        HashSet<Integer> set = new HashSet<Integer>();
        set.add(n);

        while (true) {
            while (n > 0) {
                sum = (n % 10) * (n % 10) + sum;
                n /= 10;
            }
            n = sum;
            sum = 0;

            if (n == 1) {
                return true;
            }
            if (set.contains(n)) {
                break;
            }

            set.add(n);
        }

        return false;
    }
}
```
