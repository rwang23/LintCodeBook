#Pow(x, n)

	Implement pow(x, n).

####思路
	这道题是一道数值计算的题目，因为指数是可以使结果变大的运算，所以要注意越界的问题。
	如同我在Sqrt(x)这道题中提到的，一般来说数值计算的题目可以用两种方法来解，一种是以2为基进行位处理的方法，
	另一种是用二分法。
	二分法递归

```java
public class Solution {
    public double myPow(double x, int n) {

        if (n > 0) {
            return power(x, n);
        } else {
            return 1 / power(x, -n);
        }
    }

    public double power(double x, int n) {
        if (n == 0) {
            return 1;
        }

        double half = power(x, n /2);

        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
}
```
####非递归
- 利用二进制与多项式分解，[快速幂非递归实现](https://blog.csdn.net/include_not_found_/article/details/78238093)
- 这个思想太赞了，好些这种涉及幂次的非递归写法，都可以利用这个二进制与多项式

```java
public double myPow(double x, int n) {
        // Write your code here
        boolean isNegative = false;
        if (n < 0) {
            x = 1 / x;
            isNegative = true;
            n = -(n + 1); // Avoid overflow when n == MIN_VALUE
        }

        double ans = 1, tmp = x;

        while (n != 0) {
            if (n % 2 == 1) {
                ans *= tmp;
            }
            tmp *= tmp;
            n /= 2;
        }
        
        if (isNegative) {
            ans *= x;
        }
        return ans;
    }
```
