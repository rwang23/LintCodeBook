##Plus One

29% Accepted

	Given a non-negative number represented as an array of digits, plus one to the number.

	The digits are stored such that the most significant digit is at the head of the list.

	Have you met this question in a real interview? Yes
	Example
	Given [1,2,3] which represents 123, return [1,2,4].

	Given [9,9,9] which represents 999, return [1,0,0,0].

####Tags Expand
- Array
- Math

####思路
- 用一个carry来代表进位，然后同时算出此位，如果没有进位就返回现在数组，进位才返回新数组
- time o(1) 九种情况是O(1)，只有一种是O(n)

####复杂度

	The complexity is O(1)
    f(n) = 9/10 + 1/10 * O(n-1)
     ==>  O(n) =  10 / 9 = 1.1111 = O(1)

```java
public class Solution {
    // The complexity is O(1)
    // f(n) = 9/10 + 1/10 * O(n-1)
    //  ==>  O(n) =  10 / 9 = 1.1111 = O(1)

    public int[] plusOne(int[] digits) {
        int carries = 1;
        for(int i = digits.length-1; i>=0 && carries > 0; i--){  // fast break when carries equals zero
            int sum = digits[i] + carries;
            digits[i] = sum % 10;
            carries = sum / 10;
        }
        if(carries == 0)
            return digits;

        int[] rst = new int[digits.length+1];
        rst[0] = 1;
        for(int i=1; i< rst.length; i++){
            rst[i] = digits[i-1];
        }
        return rst;
    }
}
```
