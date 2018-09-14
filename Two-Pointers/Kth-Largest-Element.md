##Kth Largest Element

19% Accepted

	Find K-th largest element in an array.

	Have you met this question in a real interview? Yes
	Example
	In array [9,3,2,4,8], the 3rd largest element is 4.

	In array [1,2,3,4,5], the 1st largest element is 5, 2nd largest element is 4, 3rd largest element is 3 and etc.

	Note
	You can swap elements in the array

####Challenge
- O(n) time, O(1) extra memory.

####Tags Expand
- Quick Sort
- Sort


####思路
- quick select
- As in quick sort, we have to do partition in halves , and then in halves of a half, but this time, we only need to do the next round partition in one single partition (half) of the two where the element is expected to lie in.
- It is like (not very accurate)
- n + 1/2 n + 1/4 n + 1/8 n + ..... < 2 n
- 找第几大,就变成了length - k 第几小问题
- partition 模板
- 在每次二分里边,都有一个半边排好了序,最后取num[k]就行了

```java
public class Solution {
    /**
     * @param n: An integer
     * @param nums: An array
     * @return: the Kth largest element
     */
    public int kthLargestElement(int k, int[] nums) {
        if (nums == null || nums.length == 0 || k < 1 || k > nums.length){
            return -1;
        }
        return partition(nums, 0, nums.length - 1, nums.length - k);
    }

    private int partition(int[] nums, int start, int end, int k) {
        if (start >= end) {
            return nums[k];
        }

        int left = start, right = end;
        int pivot = nums[(start + end) / 2];

        while (left <= right) {
            while (left <= right && nums[left] < pivot) {
                left++;
            }
            while (left <= right && nums[right] > pivot) {
                right--;
            }
            if (left <= right) {
                swap(nums, left, right);
                left++;
                right--;
            }
        }

        if (k <= right) {
            return partition(nums, start, right, k);
        }
        if (k >= left) {
            return partition(nums, left, end, k);
        }
        return nums[k];
    }    

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}

```
