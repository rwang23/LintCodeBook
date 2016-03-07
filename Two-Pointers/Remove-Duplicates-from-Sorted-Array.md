##Remove Duplicates from Sorted Array

32% Accepted

	Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

	Do not allocate extra space for another array, you must do this in place with constant memory.

	Have you met this question in a real interview? Yes
	Example
	Given input array A = [1,1,2],

    Your function should return length = 2, and A is now [1,2].

####Tags Expand
- Two Pointers Array

####思路
- 其实挺难的，需要画图通过两根指针来找规律来写
- 如果没看明白,可以看第二种解法,就会清晰明了很多,不过速度慢一倍,不过也是O(n)

```java
public class Solution {
    /**
     * @param A: a array of integers
     * @return : return an integer
     */
    public int removeDuplicates(int[] nums) {
        // write your code here
        if (nums == null || nums.length <= 1) {
            return nums.length;
        }

        int i = 0;
        int j = 1;
        while (i < nums.length && j < nums.length) {
        	/*
        	如果出现相同，则j继续向前边找，找到不同于A[i]的那个数
        	 */
            if (nums[i] == nums[j]){
                j++;
            } else {
            	/*
            	i++就是指向之前那个重复的元素，然后好用nums[j] 去替代nums[i]
            	 */
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;

    }
}

```

####更好的理解
- 先找相同值,找到了之后赋值为max_value
- 然后再遍历一遍,交换为max_value的值

```java
public class Solution {
    public int removeDuplicates(int[] nums) {

        int size = nums.length;
        if (size <= 1) {
            return size;
        }

        int i = 0;
        int j = 1;

        while (j < size) {
            while (j < size && nums[i] == nums[j]) {
                nums[j] = Integer.MAX_VALUE;
                j++;
            }

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

####写的第三种解法
- 根据第二种解法简化

```java
public class Solution {
    public int removeDuplicates(int[] nums) {

        int size = nums.length;
        if (size <= 1) {
            return size;
        }

        int i = 0;
        int j = 1;
        while (j < size) {
            while (j < size && nums[i] == nums[j]) j++;
            while (j + 1 < size && nums[j] == nums[j + 1]) j++;
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
