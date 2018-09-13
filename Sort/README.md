This is the review of subsets.

##Quick sort

```java
public void quickSort(int[] A, int start, int end) {
        if (start >= end) {
            return;
        }

        int index = rand.nextInt(end - start + 1)  + start;
        int pivot = A[index];
        int left = start;
        int right = end;
        
        while (left <= right) {
            while (left <= right && A[left] < pivot) {
                left ++;
            }
            while (left <= right && A[right] > pivot) {
                right --;
            }
            
            if (left <= right) {
                int temp = A[left];
                A[left] = A[right];
                A[right] = temp;
                
                left ++;
                right --;
            }
        }
        // A[start... right] 这里用的right的原因是right已经比left小了，用right不会重复，下面用left同理
        quickSort(A, start, right);
        // A[left ... end]
        quickSort(A, left, end);
    }
```
##Merge sort recursion
```java
private void mergeSort(int[] A, int start, int end, int[] temp) {
        if (start >= end) {
            return;
        }
        
        int left = start, right = end;
        int mid = (start + end) / 2;

        mergeSort(A, start, mid, temp);
        mergeSort(A, mid+1, end, temp);
        merge(A, start, mid, end, temp);
    }
    
    private void merge(int[] A, int start, int mid, int end, int[] temp) {
        int left = start;
        int right = mid+1;
        int index = start;
        
        // merge two sorted subarrays in A to temp array
        while (left <= mid && right <= end) {
            if (A[left] < A[right]) {
                temp[index++] = A[left++];
            } else {
                temp[index++] = A[right++];
            }
        }
        while (left <= mid) {
            temp[index++] = A[left++];
        }
        while (right <= end) {
            temp[index++] = A[right++];
        }
        
        // copy temp back to A
        for (index = start; index <= end; index++) {
            A[index] = temp[index];
        }
    }
```

##Merge Sort non-recursion
```java
```



##Different Sort
- Merge sort 是稳定排序，如果有两个2，如果2有一个属性叫做先后，那么2先能排到2后前面
- Quick sort是不稳定排序，无法实现上述
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

####另一种写法 / 推荐用这一种
```java
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
        //int mid = start + (end - start)/2;
        int lo = start;
        int pivot = nums[lo];
        start++;
        while (start <= end) {
            while (start <= end && nums[start] < pivot) {
                start++;
            }
            while (start <= end && nums[end] > pivot) {
                end--;
            }
            if (start <= end) {
                swap(nums, start, end);
                start++;
                end--;
            }
        }
        //一定要--start,因为上一次交换start已经start = start + 1,而我们需要的是没有+1的start
        swap(nums, lo, --start);
        return start;
        //index = start前的,数组元素已经小于现在的nums[start],后面的大于
    }
```

####Quick Sort Improve
![Quick Sort Improve](../image/QuickSort-Improve.png)

####Quick Select
![Quick Select](../image/QuickSelect.png)

####Quick 3 Way
![Quick 3 Way](../image/QuickSort-3Way.png)
