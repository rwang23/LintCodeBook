##Power of Four
	Total Accepted: 6767 Total Submissions: 20205 Difficulty: Easy
	Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

	Example:
	Given num = 16, return true. Given num = 5, return false.

	Follow up: Could you solve it without loops/recursion?

####思路
- 类似于power of two
- 同时因为是4,首先是power of two,所以除了第一个bit是1后面必须全部是0
- 首先是power of two,然后位数是偶数

2   10
4   100
8   1000
16  10000
32  100000
64  1000000
128 10000000
256 100000000
512 1000000000

####直接做
```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        if (num <= 0) {
            return false;
        }

        while (num > 1) {
            if (num / 4 * 4 != num) {
                return false;
            }
            num /= 4;
        }

        return true;
    }
}
```

####Bit方法

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        if (num <= 0) {
            return false;
        }

        if ((num & (num - 1)) != 0) {
            return false;
        }

        int bit = 1;
        int digit = 0;
        while (true) {
            if ((num & bit) == 0) {
                digit++;
            } else {
                digit++;
                break;
            }

            bit = bit << 1;
        }

        return digit % 2 == 1;
    }
}
```
