##递归

###1.递归的定义

###2.递归的拆解

###3.递归的出口

```
//递归版本，会超时
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
