##Power of Three

	Given an integer, write a function to determine if it is a power of three.

	Follow up:
	Could you do it without using any loop / recursion?
##思路1
- [各种方法集锦](https://leetcode.com/discuss/78532/summary-all-solutions-new-method-included-at-15-30pm-jan-8th)

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

##思路2
```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n <= 0) {
            return false;
        }

        long i = 1;
        while (i <= n) {
            if (i == n) {
                return true;
            }
            i *= 3;
        }

        return false;
    }
}
```
####思路3
```java
public class Solution {
public boolean isPowerOfThree(int n) {
    // 1162261467 is 3^19,  3^20 is bigger than int
    return ( n>0 &&  1162261467%n==0);
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
