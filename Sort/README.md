This is the review of subsets.

##Different Sort
![Different Sort](../image/Sorting-Algorithms.png)



####Two Pointers Sort
- Many problem use the two pointers to sort, the most classic one is the color sort

####Merge Sort Basic
![Merge Sort Basic](../image/MergeSort-Merge.png)

####Merge Sort Recursion
![Merge Sort Recursion](../image/MergeSort-Recursion.png)

####Merge Sort Recursion Improvement
![Merge Sort Recursion Improvement](../image/MergeSort-Recursion-Improve.png)

####Merge Sort Iterative
![Merge Sort Iterative](../image/MergeSort-Iterative.png)

####Quick Sort Basic
![Quick Sort Basic](../image/QuickSort-Sort.png)

####Quick Sort Partitioning
![Quick Sort Partitioning](../image/QuickSort-Partitioning.png)

####另一种写法
```java
class Solution{
	public void quickSort(int[] nums){
        if (nums == null || nums.length == 0) {
            return;
        }
        sortHelper(nums, 0, nums.length - 1);
    }

    public void sortHelper(int[] nums, int start, int end){
        if (start >= end) {
            return;
        }
        int partitionPoint = partition(nums, start, end);
        sortHelper(nums, start, partitionPoint - 1);
        sortHelper(nums, partitionPoint + 1, end);

    }

    public void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }

    public int partition(int[] nums, int start, int end){
        int mid = start + (end - start)/2;

        int pivot = nums[mid];
        while (start < end) {
            while (start < end && nums[start] < pivot) {
                start++;
            }
            while (start < end && nums[end] > pivot) {
                end--;
            }
            if (start < end) {
                swap(nums, start, end);
                start++;
                end--;
            }
        }
        return start;
        //index = start前的,数组元素已经小于现在的nums[start],后面的大于
    }
}
```

####Quick Sort Improve
![Quick Sort Improve](../image/QuickSort-Improve.png)

####Quick Select
![Quick Select](../image/QuickSelect.png)

####Quick 3 Way
![Quick 3 Way](../image/QuickSort-3Way.png)
