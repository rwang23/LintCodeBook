##Sqrt(x)

23% Accepted

	Implement int sqrt(int x).

	Compute and return the square root of x.

	Have you met this question in a real interview? Yes
	Example
	sqrt(3) = 1

	sqrt(4) = 2

	sqrt(5) = 2

	sqrt(10) = 3

####Challenge
O(log(x))

####Tags Expand
Binary Search Mathematics

```java
public class Solution {
    public int mySqrt(int x) {
        int start = 0;
        int end = x;
        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (mid * mid == x) {
                return mid;
            } else if ((long) mid * mid > (long) x) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if ((long) end * end <= (long) x) {
            return end;
        } else {
            return start;
        }
    }
}
```
