##Move Zeroes
[Move Zeroes](https://www.lintcode.com/problem/move-zeroes/description?_from=ladder&&fromId=1)

	Total Accepted: 78338 Total Submissions: 177188 Difficulty: Easy
	Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

	For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

	Note:
	You must do this in-place without making a copy of the array.
	Minimize the total number of operations.

####思路
- Two pointers
- 这里双指针是两种思路
- 一种就第一种解法，分别找0和非0，然后调换，要注意j<=i
- 另一种解法，就是直接找非0，然后把整个数组直接调换过去
- 第一种解法是交换了2n-1次,第二种解法只交换了n次

####思路1
```java
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return;
        }

        int i = 0; //zero index
        int j = 0; //non-zero index

        while (i < nums.length && j < nums.length) {
            while (i < nums.length && nums[i] != 0) {
                i++;
            }

            while (j < nums.length && nums[j] == 0 || j <= i) {
                j++;
            }

            if (i == nums.length || j == nums.length) {
                return;
            }

            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
        }
    }
}
```
####思路2
- 双指针,跟下面这道题很像
- [Remove Duplicate in a array](https://rwang23.gitbooks.io/lintcodebook/content/Two-Pointers/Remove-Duplicate-Numbers-in-Array.html)
```java
public class Solution {
    /**
     * @param nums: an integer array
     * @return: nothing
     */
    public void moveZeroes(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return;
        }

        int curIndex = 0;
        for (int zeroIndex = 0; zeroIndex < nums.length; zeroIndex++) {
            if (nums[zeroIndex] != 0) {
                nums[curIndex++] = nums[zeroIndex];
            }
        }

        while (curIndex < nums.length) {
            nums[curIndex++] = 0;
        }
    }
}
```
