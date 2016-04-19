##H-Index
	Total Accepted: 31273 Total Submissions: 106785 Difficulty: Medium
	Given an array of citations (each citation is a non-negative integer) of a researcher,
	write a function to compute the researcher's h-index.

	According to the definition of h-index on Wikipedia:
	"A scientist has index h if h of his/her N papers have at least h citations each,
	and the other N − h papers have no more than h citations each."

	For example, given citations = [3, 0, 6, 1, 5],
	which means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively.
	Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, his h-index is 3.

	Note: If there are several possible values for h, the maximum one is taken as the h-index.

####思路
- 直接做,利用一下greedy
- 从后往前遍历,遍历到了就是最大值,break掉
- worsest case 时间复杂度是O(n2)

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }
        int size = citations.length;
        int max = 0;
        for (int i = size - 1; i >= 0; i--) {
            int count = 0;
            for (int j = 0; j < size; j++) {
                if (citations[j] >= i + 1) {
                    count++;
                }
            }
            if (count >= i + 1) {
                max = i + 1;
                break;
            }
        }
        return max;
    }
}
```

####Sort
- 先进行sort
- 假设是 0 1 3 5 6,我们倒过来看 6 5 3 1 0,
- 让 n = size
- 如果 0 >= size,那么就是 h-index = n, 不行就继续, 同时n--
- 发现3 >= n - 3, 那么 n -3 就是我们所求
- O(nlogn)

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }
        Arrays.sort(citations);
        int size = citations.length;
        int n = size;
        for (int i = 0; i < size; i++) {
            if (citations[i] >= n) {
                return n;
            }
            n--;
        }
        return 0;
    }
}
```

####使用一个辅助数组
- 时间 O(n)
- 因为又是涉及到数据范围,并且是可以从0 - n
- 所以用一个数组来储存次数,两次loop,就找到了结果

```java
public class Solution {
    public int hIndex(int[] citations) {
        int len = citations.length;
        int[] count = new int[len + 1];

        for (int c: citations)
            if (c > len)
                count[len]++;
            else
                count[c]++;


        int total = 0;
        for (int i = len; i >= 0; i--) {
            total += count[i];
            if (total >= i)
                return i;
        }

        return 0;
    }
}
```
