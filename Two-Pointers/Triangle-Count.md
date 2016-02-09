##Triangle Count Show result

31% Accepted

	Given an array of integers, how many three numbers can be found in the array, so that we can build an triangle whose three edges length is the three numbers that we find?

	Have you met this question in a real interview? Yes
	Example
	Given array S = [3,4,6,7], return 3. They are:

	[3,4,6]
	[3,6,7]
	[4,6,7]
	Given array S = [4,4,4,4], return 4. They are:

	[4(1),4(2),4(3)]
	[4(1),4(2),4(4)]
	[4(1),4(3),4(4)]
	[4(2),4(3),4(4)]
####Tags Expand
- Two Pointers
- LintCode Copyright

####思路

####暴力解法
- 先排序,然后找
- 条件:s[i]+s[j]>s[k] && s[i]+s[k]>s[j] && s[k]+s[j]>s[i]
- 因为已经排过序了,令i>j>k,这个时候 条件1 2自动满足,只需要找s[k]+s[j]>s[i]
- O(n3) 强行破解

```java
public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int S[]) {
        // write your code here
        if (S == null || S.length < 3) {
            return -1;
        }
        Arrays.sort(S);
        int len = S.length;
        int count = 0;
        for (int i = 2; i < len; i++) {
            for (int j = 1; j < i; j++) {
                for (int k = 0; k < j; k++) {
                    if (S[j] + S[k] > S[i]) {
                        count++;
                    }
                }
            }
        }
        return count;
    }
}
```
####优化
- 从暴力解法优化
- 最后找S[j] + S[k] > S[i]
- 也就是two sum II的做法
- 两个指针进行比较

```java
public class Solution {
    /**
     * @param S: A list of integers
     * @return: An integer
     */
    public int triangleCount(int S[]) {
        // write your code here
        if (S == null || S.length <= 2) {
            return 0;
        }

        int size = S.length;
        Arrays.sort(S);
        int count = 0;

        for (int i = 2; i < size; i++) {
            int start = 0;
            int end = i - 1;
            while (start < end) {
                if (S[start] + S[end] > S[i]) {
                    count = count + end - start;
                    end--;
                } else {
                    start++;
                }
            }
        }

        return count;
    }
}


```
