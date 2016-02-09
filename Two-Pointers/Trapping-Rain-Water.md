##Trapping Rain Water

	Given n non-negative integers representing an elevation map where the width of each bar is 1,
	compute how much water it is able to trap after raining.

	Example
	Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.

####Challenge
O(n) time and O(1) memory

O(n) time and O(n) memory is also acceptable.

####Tags Expand
Two Pointers, Forward-Backward, Traversal Array

####思路

- 两根指针标准题
- 直接看题目的图形更加直观
- http://www.lintcode.com/en/problem/trapping-rain-water/
- 注意的是,volume是在每一格进行计算

```java
public class Solution {
    /**
     * @param heights: an array of integers
     * @return: a integer
     */
    public int trapRainWater(int[] heights) {
        // write your code here
        if (heights == null || heights.length <= 2) {
            return 0;
        }

        int start = 0;
        int end = heights.length - 1;
        int volume = 0;

        while (start < end) {

            int startIndex = start;
            int startHeight = heights[start];
            int endIndex = end;
            int endHeight = heights[end];

            while (heights[start] <= heights[end] && start < end) {
                start++;
                if (heights[start] < startHeight) {
                    volume = volume + startHeight - heights[start];
                } else {
                    startHeight = heights[start];
                }
            }

            while (heights[start] > heights[end] && start < end) {
                end--;
                if (endHeight > heights[end]) {
                    volume = volume + endHeight - heights[end];
                } else {
                    endHeight = heights[end];
                }
            }
        }

        return volume;
    }
}

```
