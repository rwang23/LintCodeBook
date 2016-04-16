##Wiggle Sort II

	Total Accepted: 7303 Total Submissions: 33382 Difficulty: Medium
	Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

	Example:
	(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6].
	(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].

	Note:
	You may assume all input has valid answer.

	Follow Up:
	Can you do it in O(n) time and/or in-place with O(1) extra space?

####思路
- 法1:直接sort O(nlogn)
- 法2:先用quick sort找到mid,然后根据mid来赋值,大于mid的放后面,其余的放前面,等于的放中间,然后用3-way partition来O完成
- 3-way partition就类似于sort color,很棒的思想

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }

        int n = nums.length;
        int mid = findMid(nums);
        int start = 0;
        int end = n - 1;
        int midIndex = 0;
        while (midIndex < end) {
            if (nums[midIndex] < mid) {
                swap(nums, midIndex++, start++);
            } else if (nums[midIndex] > mid ) {
                swap(nums, midIndex , end--);
            } else {
                midIndex++;
            }
        }

        int[] temp = new int[n];
        System.arraycopy(nums, 0, temp, 0, n);

        start = (n - 1) / 2;
        end = n - 1;

        for (int i = 0; i < n; i++) {
            if ((i & 1) == 0) {
                nums[i] = temp[start];
                start--;
            } else {
                nums[i] = temp[end];
                end--;
            }
        }
    }

    public int findMid(int[] nums) {
        if (nums == null || nums.length == 0) {
            return -1;
        }
        int start = 0;
        int end = nums.length - 1;
        int mid = start + (end - start) / 2;
        while (start < end) {
            int k = partition(nums, start, end);

            if (k == mid) {
                return nums[mid];
            } else if (k > mid) {
                end = k - 1;
            } else {
                start = k + 1;
            }
        }
        return nums[mid];
    }

    public int partition(int[] nums, int start, int end) {
        int pivot = nums[start];
        int i = start + 1;
        int j = end;

        while (i <= j) {
            while (i <= j && nums[i] < pivot) {
                i++;
            }
            while (i <= j && nums[j] > pivot) {
                j--;
            }
            if (i > j) {
                break;
            }
            swap(nums, i++, j--);
        }
        swap(nums, start, i - 1);

        return i - 1;
    }

    public void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}
```
