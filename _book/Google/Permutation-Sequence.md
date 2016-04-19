##Permutation Sequence

25% Accepted

	Given n and k, return the k-th permutation sequence.

	Have you met this question in a real interview? Yes
	Example
	For n = 3, all permutations are listed as follows:

	"123"
	"132"
	"213"
	"231"
	"312"
	"321"
	If k = 4, the fourth permutation is "231"

####Note
n will be between 1 and 9 inclusive.

####Challenge
O(n*k) in time complexity is easy, can you do it in O(n^2) or less?

####Tags Expand
Permutation Array

####思路

	同样先通过举例来获得更好的理解。以n = 4，k = 9为例：

	1234
	1243
	1324
	1342
	1423
	1432
	2134
	2143
	2314  <= k = 9
	2341
	2413
	2431
	3124
	3142
	3214
	3241
	3412
	3421
	4123
	4132
	4213
	4231
	4312
	4321

	最高位可以取{1, 2, 3, 4}，而每个数重复3! = 6次。所以第k=9个permutation的s[0]为{1, 2, 3, 4}中的第9/6+1 = 2个数字s[0] = 2。

	而对于以2开头的6个数字而言，k = 9是其中的第k' = 9%(3!) = 3个。而剩下的数字{1, 3, 4}的重复周期为2! = 2次。所以s[1]为{1, 3, 4}中的第k'/(2!)+1 = 2个，即s[1] = 3。

	对于以23开头的2个数字而言，k = 9是其中的第k'' = k'%(2!) = 1个。剩下的数字{1, 4}的重复周期为1! = 1次。所以s[2] = 1.

	对于以231开头的一个数字而言，k = 9是其中的第k''' = k''/(1!)+1 = 1个。s[3] = 4


```java
public class Solution {
	public String getPermutation(int n, int k) {

		// initialize all numbers
		ArrayList<Integer> numberList = new ArrayList<Integer>();
		for (int i = 1; i <= n; i++) {
			numberList.add(i);
		}

		// change k to be index
		k--;

		// set factorial of n
		int mod = 1;
		for (int i = 1; i <= n; i++) {
			mod = mod * i;
		}

		String result = "";

		// find sequence
		for (int i = 0; i < n; i++) {
			mod = mod / (n - i);
			// find the right number(curIndex) of
			int curIndex = k / mod;
			// update k
			k = k % mod;

			// get number according to curIndex
			result += numberList.get(curIndex);
			// remove from list
			numberList.remove(curIndex);
		}

		return result.toString();
	}
}
```
