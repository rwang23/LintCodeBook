##Prime Factorization

  Prime factorize a given integer.

##Example

  Given 10, return [2, 5].

  Given 660, return [2, 2, 3, 5, 11].

  Notice
  You should sort the factors in ascending order.
  
##思路

```java
public class Solution {
    /**
     * @param num an integer
     * @return an integer array
     */
    public List<Integer> primeFactorization(int num) {
        List<Integer> factors = new ArrayList<Integer>();

        for (int i = 2; i * i <= num; i++) {
            while (num % i == 0) {
                num = num / i;
                factors.add(i);
            }
        }
        
        if (num != 1) {
            factors.add(num);
        }
        
        return factors;
    }
}
```
