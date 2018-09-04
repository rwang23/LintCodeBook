##递归

###1.递归的定义

###2.递归的拆解

###3.递归的出口

```
//递归版本，会超时
//超时的原因是过量的重复计算，每次都要计算f(n-1) f(n-2)
//所以要么把这些计算过的值存起来，要么用循环替代此递归
public class Solution {
    /*
     * @param : an integer
     * @return: an ineger f(n)
     */
     //1.递归的定义
    public int fibonacci(int n) {
        // write your code here
        //3.递归的出口
        if (n == 1) {
            return 0;
        }
        
        if (n == 2) {
            return 1;
        }
        //2.递归的拆解
        return fibonacci(n - 1) + fibonacci(n - 2);
    }
};
```
