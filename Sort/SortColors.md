##Sort Colors

33% Accepted

	Given an array with n objects colored red, white or blue,
    sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

	Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

	Example
	Given [1, 0, 1, 2], return [0, 1, 1, 2].

####Note
You are not suppose to use the library's sort function for this problem.

####Challenge
A rather straight forward solution is a two-pass algorithm using counting sort. First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?

####Tags Expand
Two Pointers Sort Array

####Staight Forward Solution
```java
class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2
     * @return: nothing
     */
    public void sortColors(int[] nums) {
        // write your code here
        int red = 0, white = 0, blue = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                red++;
            }
            if (nums[i] == 1) {
                white++;
            }
            if (nums[i] == 2) {
                blue++;
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (i < red) {
                nums[i] = 0;
            } else if (i < red + white) {
                nums[i] = 1;
            } else if (i < red + white + blue) {
                nums[i] = 2;
            }
        }
    }
}
```

####Better Solution
    用i记录0应该放的位置，j记录2应该放的位置。
    cur从0到j扫描，
    遇到0，放在i位置，i后移；
    遇到2，放在j位置，j前移；
    遇到1，cur后移。

```java
class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2
     * @return: nothing
     */
    public void sortColors(int[] A) {

        int red = 0;
        int blue = A.length-1;
        for (int i = 0; i <= blue && i < A.length;) {
            if (A[i] == 0 && i > red ) {
                swap(A, i, red++);
            } else if (A[i] == 2 && i <= blue)
                swap(A, i, blue--);
            else
                i++;
        }
    }

    private void swap(int A[], int a, int b) {
        int temp = A[a];
        A[a] = A[b];
        A[b] = temp;
    }
}

```

