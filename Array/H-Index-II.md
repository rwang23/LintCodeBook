##H-Index II
	Total Accepted: 21748 Total Submissions: 66934 Difficulty: Medium
	Follow up for H-Index: What if the citations array is sorted in ascending order? Could you optimize your algorithm?

####思路
- 利用sort

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }
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

####二分查找
- 已经sort了,那么就要找 citations[i] >= size - i,
- 搜索的话,就能想到二分查找
- O(nlogn)

```java
public class Solution {
    public int hIndex(int[] citations) {
        if (citations == null || citations.length == 0) {
            return 0;
        }
        int size = citations.length;
        // for (int i = 0; i < size; i++) {
        //     if (citations[i] >= size - i) {
        //         return size - i;
        //     }
        // }
        int start = 0;
        int end = size - 1;

        while (start < end - 1) {
            int mid = start + (end - start) / 2;
            if (citations[mid] >= size - mid) {
                end = mid;
            } else {
                start = mid;
            }
        }
        if (citations[start] >= size - start) {
            return size - start;
        }
        if (citations[end] >= size - end) {
            return size - end;
        }
        return 0;
    }
}
```
