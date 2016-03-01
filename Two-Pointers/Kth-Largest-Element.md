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
- As in quick sort, we have to do partition in halves *, and then in halves of a half, but this time, we only need to do the next round partition in one single partition (half) of the two where the element is expected to lie in.
- It is like (not very accurate)
- n + 1/2 n + 1/4 n + 1/8 n + ..... < 2 n

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {

        int kthSmallest = nums.length - k;

        int start = 0;
        int end = nums.length - 1;

        while (start < end) {
            int p = partition(nums, start, end);

            if (p == kthSmallest) {
                return nums[p];
            } else if (p > kthSmallest) {
                end = p - 1;
            } else {
                start = p + 1;
            }
        }

        return nums[kthSmallest];
    }

    public int partition(int[] nums, int start, int end) {

        int origin = start;
        int pivot = nums[start++];

        while (start <= end) {
            while (start <= end && nums[start] < pivot) {
                start++;
            }
            while (start<=end && nums[end] > pivot) {
                end--;
            }

            if (start <= end) {
                swap(nums, start, end);
                start++;
                end--;
            }
        }

        swap(nums, origin, --start);
        return start;
    }

    public void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}

```
