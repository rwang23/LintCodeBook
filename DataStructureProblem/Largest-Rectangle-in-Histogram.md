##Largest Rectangle in Histogram

24% Accepted

	Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![histogram_area](../image/histogram_area.png)

	Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].


	The largest rectangle is shown in the shaded area, which has area = 10 unit.

	Example
	Given height = [2,1,5,6,2,3],
	return 10.

####Tags Expand
- Array
- Stack

####暴力O(n2)不会通过的方法
```java
public class Solution {
    /**
     * @param height: A list of integer
     * @return: The area of largest rectangle in the histogram
     */
    public int largestRectangleArea(int[] height) {
        // write your code here
        int maxarea = 0;
        for (int i = 0; i < height.length; i++) {
            int min = Integer.MAX_VALUE;
            for (int j = i; j >= 0; j--) {
                min = Math.min(min, height[j]);
                maxarea = Math.max(min * (i - j + 1), maxarea);
            }
        }
        return maxarea;
    }
}

```

####高级解法
- [思路来源](http://www.cnblogs.com/legendmaner/archive/2013/04/18/3028748.html)
- 单调栈，顾名思义就是说栈内的元素，按照某种方式排序下，必须是单调的。如果新入栈的元素破坏了单调性，就弹出栈内元素，知道满足单调性。它可以很方便地求出某个数的左边或者右边第一个比它大或者小的元素，而且总时间复杂度O(N)。
- 要想找到里面的最大的面积，一定会有这么一种情况，得出的矩形的高度一定为所包含的某一个高度一致的。所以我们可以对某一个柱子的高度为标准，尽量的向两头扩展，这样就可以找出以它高度为标准的，并包含它本身的最大矩形。然后对每一个柱子都做类似的工作，最后挑出里面最大的矩形
- 所以如果我们从第一个开始计算到第n个，计算到i时，如果我们可以快速的找出左边第一个（这里第一的意思是离i最近）的比i的高度小的，就可以完成了向左扩展的工作，而向右扩展，我们本来就是一直向右走，所以直接扩展。这时候就轮到：单调栈出场了！

####改进后的算法，debug了一个半小时
- 重写
- stack push进去的是index，因为再找边界的时候找的是下标i, value的值可以直接height[i]
- 在最后已经遍历完，栈底只剩下一个数时候，强行进入pop阶段而不是push，所以用了int cur = (i == height.length) ? -1 : height[i];
- 非常巧妙的办法

```java
public class Solution {

    public int largestRectangleArea(int[] height) {
        // write your code here
        if (height == null || height.length == 0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<Integer>();
        stack.push(0);
        int maxArea = 0;
        int i = 1;
        //for (int i = 1; i <= height.length;)
        //本来写的for循环，更好理解
        //优化改为while
        while (i <= height.length) {
            int cur = (i == height.length) ? -1 : height[i];
            if (stack.isEmpty() || cur >= height[stack.peek()]) {
                stack.push(i);
                i++;
            } else {
                int thisIndex = stack.pop();
                int thisHeight = height[thisIndex];
                int startIndex;
                //考虑到pop后的边界情况
                if (!stack.isEmpty()) {
                    startIndex = stack.peek();
                } else {
                    startIndex = -1;
                }
                maxArea = Math.max(maxArea, thisHeight * (i - startIndex - 1));
            }
        }
        return maxArea;
    }
}




```
