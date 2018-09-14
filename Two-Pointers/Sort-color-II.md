## Sort Colors II

  Given an array of n objects with k different colors (numbered from 1 to k), sort them so that objects of the same color are adjacent, with the colors in the order 1, 2, ... k.

###Example
Given colors=[3, 2, 2, 1, 4], k=4, your code should sort colors in-place to [1, 2, 2, 3, 4].

###Challenge
A rather straight forward solution is a two-pass algorithm using counting sort. That will cost O(k) extra memory. Can you do it without using extra memory?

###Notice
You are not suppose to use the library's sort function for this problem.
k <= n

###思路
- 跟Move-Zeros的思路是一样的
- 使用了通向双指针
- 每次找到想找的color(1-k)其中一个,
- 然后双指针,一个在最开始需要填补的地方,一个区找数字,找到了就替换过来,这样遍历一遍
- 时间复杂度O(k*n), 这样就比sort省下了一些时间

```Java
public class Solution {
    /**
     * @param colors: A list of integer
     * @param k: An integer
     * @return: nothing
     */
    public void sortColors2(int[] colors, int k) {
        // write your code here
        if (colors == null || colors.length < k) {
            return;
        }

        int left = 0;
        for (int color = 1; color <= k; color++) {
            for (int right = 0; right < colors.length; right++) {
                if (colors[right] == color) {
                    swap(colors, left++, right);
                }
            }

        }
    }

    public void swap(int[] num, int index1, int index2) {
        int temp = num[index1];
        num[index1] = num[index2];
        num[index2] = temp;
    }
}
```
