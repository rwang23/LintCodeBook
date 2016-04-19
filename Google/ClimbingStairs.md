####Climbing Stairs

39% Accepted

	You are climbing a stair case. It takes n steps to reach to the top.

	Each time you can either climb 1 or 2 steps.
    In how many distinct ways can you climb to the top?

	Have you met this question in a real interview? Yes
	Example
	Given an example n=3 , 1+1+1=2+1=1+2=3

	return 3

####Tags Expand
- Dynamic Programming

####思路
- 因为只是n，所以不能数组，用三个int去存值就可以了
- f(n) = f(n-1) + f(n-2)
- 状态 初始化 循环方程 结果


```java
public class Solution {
    /**
     * @param n: An integer
     * @return: An integer
     */
    public int climbStairs(int n) {
        // write your code here
        if( n <= 1){
            return 1;
        }
        int lastlast = 1;
        int last = 1;
        int now = 0;

        for( int i = 2; i <= n; i++){
            now = last + lastlast;
            lastlast = last;
            last = now;
        }
        return now;
    }
}

```
