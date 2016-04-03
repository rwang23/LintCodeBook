##Find Minimum in Rotated Sorted Array II

38% Accepted

	Suppose a sorted array is rotated at some pivot unknown to you beforehand.

	(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

	Find the minimum element.

	The array may contain duplicates.

	Have you met this question in a real interview? Yes
	Example
	Given [4,4,5,6,7,0,1,2] return 0

####Tags Expand
- Binary Search
- Divide and Conquer

####思路
- 构想极端情况 [1,1,1,1,1,1,1,1]
- 极端情况下 二分法也没用，找不到前面的，所以必须遍历
- 同理 Search in Rotated Sorted Array II 也是这么处理

```java
public class Solution {
    public int findMin(int[] num) {
        int min = num[0];
        for (int i = 1; i < num.length; i++) {
            if (num[i] < min)
                min = num[i];
        }
        return min;
    }
}
```

####然而其实也可以使用二分方法，最坏情况是o(n)

    正常情况二分法是没问题的
    比如33333012
    或者345671111
    但是出现了前面后面都相等的情况就不行了

    3 1 2 3 3 3 3
    3 3 3 3 1 2 3

    但可以肯定的是可以排除A[end]：因为即使min = A[end]，
    由于A[end] = A[mid]，排除A[end]并没有让min丢失。所以增加的条件是：

    A[mid] = A[end]：搜索A[start : end-1]

- 出现最前面和末尾一样的情况,比如3,3,3,2,3,3,3
- 如果相等,就不能判断在前面还是后面了,所以直接end--

```java
public class Solution {
    public int findMin(int[] num) {
        int start = 0, end = num.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (num[mid] > num[end]) {
                start = mid;
            } else if (num[mid] < num[end]) {
                end = mid;
            /*
            因为是以num[end]作为参照物的，所以比较num[mid] = num[end]
            如果是以num[start]作为参照物，那么就是比较num[mid]与mun[start]
             */
            } else if (num[mid] == num[end]) {
                end--;
            }
        }
        if (num[start] < num[end]) {
            return num[start];
        } else {
            return num[end];
        }
    }
}
```
