##Drop Eggs

  There is a building of n floors. If an egg drops from the k th floor or above, it will break. If it's dropped from any floor below, it will not break.

  You're given two eggs, Find k while minimize the number of drops for the worst case. Return the number of drops in the worst case.

##Example
  Given n = 10, return 4.
  Given n = 100, return 14.

#Clarification
  
  For n = 10, a naive way to find k is drop egg from 1st floor, 2nd floor ... kth floor. But in this worst case (k = 10), you have to drop 10 times.

  Notice that you have two eggs, so you can drop at 4th, 7th & 9th floor, in the worst case (for example, k = 9) you have to drop 4 times.
  
##思路
- 肯定按最安全的办法扔，那么一次就能慢慢往上增加的楼层数
- 其实就是求x : x + (x - 1) + (x - 2)+ ... + 1 > = n, 即 (x + 1) * x / 2 >= n


```java
public class Solution {
    /**
     * @param n: An integer
     * @return: The sum of a and b
     */
    public int dropEggs(int n) {
        // write your code here
        
        long start = 1;
        long end = n;
        while (start + 1 < end) {
            long mid = start + (end - start) / 2;
            if (mid * (mid + 1) / 2 >= n) {
                end = mid;
            } else {
                start = mid;
            } 
        }
        
        if (start * (start + 1) / 2 >= n) {
            return (int)start;
        } else {
            return (int)end;
        }
    }
}
```
