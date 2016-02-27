##Power of Three

	Given an integer, write a function to determine if it is a power of three.

	Follow up:
	Could you do it without using any loop / recursion?
##思路

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) {
            return false;
        }


        while (n > 1) {
            if (n / 3 * 3 != n) {
                return false;
            }
            n /= 3;
        }

        return true;
    }
}
```

##最简单方法
###对数换底公式

				logn(b)
	loga(b) = 	-------
				logn(a)

```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) {
            return false;
        }

        return n <= 0 ? false : n == Math.pow(3, Math.round(Math.log(n) / Math.log(3)));
    }
}
```
