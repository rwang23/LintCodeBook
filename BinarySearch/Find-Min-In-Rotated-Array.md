##Find Minimum in Rotated Sorted Array

33% Accepted

	Suppose a sorted array is rotated at some pivot unknown to you beforehand.

	(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

	Find the minimum element.

	Have you met this question in a real interview? Yes
	Example
	Given [4, 5, 6, 7, 0, 1, 2] return 0

####Note

    You may assume no duplicate exists in the array.

####Tags Expand
- Binary Search

####思路
- 解法来自九章，自己写的有点冗长，在while中循环的条件很重要
- 通过判断与end的关系就可以，然而自己判断num[mid]与num[mid-1]，这样也导致了需要考虑mid-1的边界条件


```java
public class Solution {
    public int findMin(int[] num) {
        int start = 0, end = num.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (num[mid] >= num[end]) { //这个=号不要也可以，因为不会有这种情况
                start = mid;
            } else {
                end = mid;
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
