##Remove Duplicates from Sorted Array II

30% Accepted

	Follow up for "Remove Duplicates":
	What if duplicates are allowed at most twice?

	For example,
	Given sorted array A = [1,1,1,2,2,3],

	Your function should return length = 5, and A is now [1,1,2,2,3].


####Tags Expand
- Two Pointers Array

####思路
- 来自于I 的第二种解法
- 也可以从第三种解法改造,但是第二种很容易理解和操作

```java
public class Solution {
    public int removeDuplicates(int[] nums) {

        int size = nums.length;
        int i = 0;
        int j = 1;
        int count = 1;
        while (j < size) {
            if (j < size && count <= 1 && nums[i] == nums[j]) {
                count++;
                i++;
                j++;
            }
            while (j < size && count >= 2 && nums[i] == nums[j]) {
                nums[j] = Integer.MAX_VALUE;
                j++;
            }
            count = 1;
            i = j;
            j++;
        }

        i = 0;
        j = 1;

        while (j < size) {
            while (j < size && nums[j] == Integer.MAX_VALUE) j++;
            if (j >= size) break;
            swap(nums, ++i, j++);
        }

        return i + 1;
    }

    public void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}
```
