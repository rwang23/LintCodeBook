##Minimum Adjustment Cost

	Given an integer array, adjust each integers
	so that the difference of every adjacent integers are not greater than a given number target.

	If the array before adjustment is A, the array after adjustment is B, you should minimize the sum of |A[i]-B[i]|

	Example
	Given [1,4,2,3] and target = 1, one of the solutions is [2,3,2,3], the adjustment cost is 2 and it's minimal.

	Return 2.

####Note
You can assume each number in the array is a positive integer and not greater than 100.

####Tags Expand
LintCode Copyright Dynamic Programming Backpack

####思路
- [参考来源](http://www.cnblogs.com/EdwardLiu/p/4385819.html)
- 重做

####解释


	定义result[i][j] 表示前 i个number 要变成最后一个number是j的数字，这样的minimum adjusting cost

	如果第i-1个数是j, 那么第i-2个数只能在[lowerRange, UpperRange]之间，lowerRange=Math.max(0, j-target), upperRange=Math.min(99, j+target),

	这样的话，状态方程：

    for (int p = lowerRange; p <= upperRange; p++) {
        result[i][j] = Math.min(result[i][j], result[i - 1][p]+Math.abs(j - A.get(i-1)));
    }
####代码
```java
public class Solution {
    /**
     * @param A: An integer array.
     * @param target: An integer.
     */
    public int MinAdjustmentCost(ArrayList<Integer> A, int target) {
        // write your code here
        if (A.isEmpty() || A.size() <= 1) {
            return 0;
        }

        int[][] result = new int[A.size() + 1][100];
        int min = Integer.MAX_VALUE;

        for (int j = 0; j <= 99; j++) {
            result[0][j] = 0;
        }
        for (int i = 1; i <= A.size(); i++) {
            for (int j = 0; j <= 99; j++) {
                result[i][j] = Integer.MAX_VALUE;
                int lowerRange = Math.max(0, j - target);
                int upperRange = Math.min(99, j + target);
                for (int p = lowerRange; p <= upperRange; p++) {
                    result[i][j] = Math.min(result[i][j], result[i - 1][p]+Math.abs(j - A.get(i-1)));
                }
            }
        }
        for (int j = 0; j <= 99; j++) {
            min = Math.min(min, result[A.size()][j]);
        }
        return min;
    }
}
```

