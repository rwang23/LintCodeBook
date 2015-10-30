##Product of Array Exclude Itself

25% Accepted

	Given an integers array A.

	Define B[i] = A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1],
	calculate B WITHOUT divide operation.

	Have you met this question in a real interview? Yes
	Example
	For A = [1, 2, 3], return [6, 3, 2].

####Tags Expand
- Forward-Backward Traversal
- LintCode Copyright


####暴力 O(n2) 解法， 并没有什么用
```java
public class Solution {
    /**
     * @param A: Given an integers array A
     * @return: A Long array B and B[i]= A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]
     */
    public ArrayList<Long> productExcludeItself(ArrayList<Integer> A) {
        // write your code
        ArrayList<Long> result = new ArrayList<Long>();
        for (int i = 0; i < A.size(); i++) {
            long B = 1;
            for (int j = 0; j < A.size(); j++) {
                if (j != i) {
                    B = B *  A.get(j);
                }
            }
            result.add(B);
        }
        return result;
    }
}
```

####O(n)解法
- 前后夹击，空间换时间，把前边每一个product算出来，后边每一个算出来
- left_product[i] 表示i前边的数的积
- right_product[i] 表示i后边的数的积
- 再一个for循环，去给result添加值

```java
public class Solution {
    /**
     * @param A: Given an integers array A
     * @return: A Long array B and B[i]= A[0] * ... * A[i-1] * A[i+1] * ... * A[n-1]
     */
    public ArrayList<Long> productExcludeItself(ArrayList<Integer> A) {
        // write your code
        if ( A == null || A.size() == 0) {
            return null;
        }
        ArrayList<Long> result = new ArrayList<Long>();
        long[] left_product = new long[A.size()];
        long[] right_product = new long[A.size()];

        left_product[0] = 1;
        for (int i = 1; i < A.size(); i++) {
            left_product[i] = left_product[i - 1] * A.get(i - 1);
        }

        right_product[A.size() - 1] = 1;
        for (int i = A.size() - 2; i >= 0; i--) {
            right_product[i] = right_product[i + 1] * A.get(i + 1);
        }

        for (int i = 0; i < A.size(); i++) {
            result.add(left_product[i] * right_product[i]);
        }

        return result;
    }
}


```
