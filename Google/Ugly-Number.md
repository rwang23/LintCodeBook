##Ugly Number

	Ugly number is a number that only have factors 3, 5 and 7.

	Design an algorithm to find the Kth ugly number.
	The first 5 ugly numbers are 3, 5, 7, 9, 15 ...

	Have you met this question in a real interview? Yes
	Example
	If K=4, return 9.

####Challenge
O(K log K) or O(K) time.

####Tags Expand
LintCode Copyright Priority Queue


####思路
-[参考来源](http://blog.csdn.net/nisxiya/article/details/46767595)

	解法一：时间复杂度O(k log k)，空间复杂度O(k)

	使用priority_queue模拟最小堆： 从中取出最小的 ugly number , 然后该 ugly number 分别乘以3, 5, 7 然后又放进 priority_queue中
	如果上述过程中，将乘以3,5,7之后的数直接放入 priority_queue 将可能导致重复放入的问题，比如：当取出 9， 然后放入27, 45, 63,。后面当取出 21 时，放入 63, 105, 147，这里就重复放入 63 了。因此需要用个 hashset来 mark 哪些元素已经放入过了。
	时间复杂度分析：共 k 个元素，每次取出一个元素时，都需要对堆进行操作，时间复杂度为 O(k)，因此时间复杂度为 O(k log k).

	解法二：动规方法 时间复杂度 O(k)，空间复杂度O(k)

	使用 primes 数组来记录前 k 个ugly_number。在生成 primes 数组时，新增入的元素，肯定是该 primes 数组中前面某些元素乘以3，或是乘以5，或是乘以7的结果，且是最小的。

	丑陋数序列可以拆分为下面3个子列表：

	(1) 3×3, 5×3, 7×3, 9×3, 15×3, …
	(2) 3×5, 5×5, 7×5, 9×5, 15×5, …
	(3) 3×7, 5×7, 7×7, 9×7, 15×7, …
	我们可以发现每一个子列表都是丑陋数本身 乘以 3, 5, 7

	接下来我们使用与归并排序相似的合并方法，从3个子列表中获取丑陋数。每一步我们从中选出最小的一个，然后向后移动一步。

```java

class Solution {
    /**
     * @param k: The number k.
     * @return: The kth prime number as description.
     */
    public long kthPrimeNumber(int k) {
        // write your code here
        if (k <= 0) {
            return -1;
        }

    	long[] uglyNumbers = new long[k + 1];
    	int indexFor3 = 0, indexFor5 = 0, indexFor7 = 0; //multiplier index
    	uglyNumbers[0] = 1;

    	for (int i = 1; i <= k; i++) {
    		uglyNumbers[i] = Math.min(Math.min(3 * uglyNumbers[indexFor3], 5 * uglyNumbers[indexFor5]), 7 * uglyNumbers[indexFor7]);
    		if (uglyNumbers[i] == 3 * uglyNumbers[indexFor3]) {
				indexFor3++;
    		}
    		if (uglyNumbers[i] == 5 * uglyNumbers[indexFor5]) {
    			indexFor5++;
    		}
    		if (uglyNumbers[i] == 7 * uglyNumbers[indexFor7]) {
    			indexFor7++;
    		}
    	}

    	return uglyNumbers[k];
    }
}
```
