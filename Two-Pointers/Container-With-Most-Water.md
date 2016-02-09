##Container With Most Water

38% Accepted

	Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

	Have you met this question in a real interview? Yes
	Example
	Given [1,3,2], the max area of the container is 2.

	Note
	You may not slant the container.

####Tags Expand
- Two Pointers Array

####暴力O(n2)解法
```java
public class Solution {
    /**
     * @param heights: an array of integers
     * @return: an integer
     */
    public int maxArea(int[] heights) {
        // write your code here
        if (heights == null || heights.length == 0) {
            return 0;
        }
        int size = heights.length;
        int max = Integer.MIN_VALUE;
        for (int i = 1; i < size; i++) {
            for (int j = 0; j < i; j++) {
                int area = (i - j) * Math.min(heights[i], heights[j]);
                max = Math.max(area, max);
            }
        }
        return max;
    }
}
```


####优化解法
    先从暴力解法开始思考
    无非就是要忽略掉一些情况
    假设 [2,1,4,6,2,3]
    考虑 [2,3]的情况
    此时 end = 5, left = 0, area = (5-0) * min(2,3) = 10
    这个时候还需要考虑 end = 4/3/2/1的情况嘛?
    也就是 [2,2] [2,6] [2,4] [2,1]的情况?
    完全不用,因为end=5 left=0时候, 2<3, 上述情况不会让area比10大了

    反之,考虑height[end] > height[start]的情况

    这样,就优化到了O(n)

```java
public class Solution {
    /**
     * @param heights: an array of integers
     * @return: an integer
     */
    public int maxArea(int[] heights) {
        // write your code here
        if (heights == null || heights.length < 2) {
            return 0;
        }

        int start = 0;
        int end = heights.length - 1;
        int max = 0;

        while (start < end) {
            while (heights[start] <= heights[end] && start < end) {
                max = Math.max(max, (end - start) * heights[start]);
                start++;
            }
            while (heights[start] > heights[end] && start < end) {
                max = Math.max(max, (end - start) * heights[end]);
                end--;
            }
        }

        return max;

    }
}

```
