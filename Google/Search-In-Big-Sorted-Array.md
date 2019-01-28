##Search in a Big Sorted Array

39% Accepted

```
Given a big sorted array with non-negative integers sorted by non-decreasing order. The array is so big so that you can not get the length of the whole array directly, and you can only access the kth number by ArrayReader.get(k) (or ArrayReader->get(k) for C++). Find the first index of a target number. Your algorithm should be in O(log k), where k is the first index of the target number.

Return -1, if the number doesn't exist in the array.

Example
Given [1, 3, 6, 9, 21, ...], and target = 3, return 1.

Given [1, 3, 6, 9, 21, ...], and target = 4, return -1.

Challenge
O(log k), k is the first index of the given target number.

Notice
If you accessed an inaccessible index (outside of the array), ArrayReader.get will return 2,147,483,647.

```

####Challenge
O(log k), k is the first index of the given target number.

####Tags Expand
- Binary Search
- Sorted Array

####思路
- 要求O(logk) 那么就去想如何才能logK,只有对原数进行倍增的办法
- 剩下的也就是二分搜索



```java
public class Solution {
    /*
     * @param reader: An instance of ArrayReader.
     * @param target: An integer
     * @return: An integer which is the first index of target.
     */
    public int searchBigSortedArray(ArrayReader reader, int target) {
        // write your code here

        int index = 1;

        while (reader.get(index) != 2147483647 && reader.get(index) < target) {
            index = index * 2;
        }

        int end = index;
        int start = index / 2;

        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (reader.get(mid) >= target) {
                end = mid;
            } else {
                start = mid;
            }
        }

        if (reader.get(start) == target) {
            return start;
        } else if (reader.get(end) == target) {
            return end;
        }

        return -1;
    }
}

```
