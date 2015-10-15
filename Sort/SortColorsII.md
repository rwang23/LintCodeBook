##Sort Colors II

32% Accepted

	Given an array of n objects with k different colors (numbered from 1 to k), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

	Have you met this question in a real interview? Yes
	Example
	Given colors=[3, 2, 2, 1, 4], k=4, your code should sort colors in-place to [1, 2, 2, 3, 4].

	Note
	You are not suppose to use the library's sort function for this problem.

####Challenge
A rather straight forward solution is a two-pass algorithm using counting sort. That will cost O(k) extra memory. Can you do it without using extra memory?

####Tags Expand
- Two Pointers
- Sort


####思路
- 跟sort color类似，用两个指针分别表针前后
- 先梳理最小值与最大值，然后次小值与次大值，依次类推

```java
class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        int start = 0;
        int end = colors.length - 1;
        for (int i = 0; i < k / 2; i++) {
            for (int j = start; j <= end && j < colors.length;) {
                if (colors[j] == i + 1 && j > start) {
                    swap(colors, j, start++);
                } else if (colors[j] == k - i && j <= end) {
                    swap(colors, j, end--);
                } else {
                    j++;
                }
            }
        }
    }
    public void swap(int[] color, int a, int b) {
        int temp = color[a];
        color[a] = color[b];
        color[b] = temp;
    }
}


```
