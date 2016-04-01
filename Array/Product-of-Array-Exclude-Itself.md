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
- 设置left right的时候 定义先设置好,这样好考虑边界条件
- 比如left[i] 表示 前i-1个数的乘积 right[i] 后i+1个数的乘积

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

####Leetcode
```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int len = nums.length;
        int[] left = new int[len];
        int[] right = new int[len];
        left[0] = nums[0];
        right[len - 1] = nums[len - 1];
        for (int i = 1; i < len; i++) {
            left[i] = left[i - 1] * nums[i];
        }
        for (int i = len - 2; i >= 0; i--) {
            right[i] = right[i + 1] * nums[i];
        }

        int[] result = new int[len];
        result[0] = right[1];
        result[len - 1] = left[len - 2];
        for (int i = 1; i < len - 1; i++) {
            result[i] = left[i - 1] * right[i + 1];
        }
        return result;
    }
}
```

####空间优化
- 左边过一遍,先留着左边相乘的值
- 再过一遍右边,从头开始计算右边相乘的值,存在end里

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int len = nums.length;
        int[] result = new int[len];

        result[0] = 1;
        for (int i = 1; i < len; i++) {
            result[i] = result[i - 1] * nums[i - 1];
        }

        int end = 1;
        for (int i = len - 2; i >= 0; i--) {
            end *= nums[i + 1];
            result[i] *= end;
        }

        return result;
    }
}
```
