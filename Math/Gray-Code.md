##Gray Code

33% Accepted
	The gray code is a binary numeral system where two successive values differ in only one bit.

	Given a non-negative integer n representing the total number of bits in the code,
	find the sequence of gray code. A gray code sequence must begin with 0 and with cover all 2n integers.


	Example
	Given n = 2, return [0,1,3,2]. Its gray code sequence is:

	00 - 0
	01 - 1
	11 - 3
	10 - 2
	Note
	For a given n, a gray code sequence is not uniquely defined.

	[0,2,3,1] is also a valid gray code sequence according to the above definition.

####Challenge
O(2n) time.

####思路
- (wiki)[https://zh.wikipedia.org/wiki/格雷码]
- 找到规律，对每一个n，都是在n-1的基础上得到的
- 原来n-1的结果在最高位加1，并reverse

```java
public class Solution {
    public ArrayList<Integer> grayCode(int n) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        if (n <= 1) {
            for (int i = 0; i <= n; i++){
                result.add(i);
            }
            return result;
        }
        result = grayCode(n - 1);
        ArrayList<Integer> r1 = reverse(result);
        int x = 1 << (n-1);
        for (int i = 0; i < r1.size(); i++) {
            r1.set(i, r1.get(i) + x);
        }
        result.addAll(r1);
        return result;
    }

    public ArrayList<Integer> reverse (ArrayList<Integer> r) {
        ArrayList<Integer> rev = new ArrayList<Integer>();
        for (int i = r.size() - 1; i >= 0; i--) {
            rev.add(r.get(i));
        }
        return rev;
    }
}
```
