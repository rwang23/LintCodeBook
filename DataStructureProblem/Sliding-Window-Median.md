##Sliding Window Median


	Given an array of n integer, and a moving window(size k),
	move the window at each iteration from the start of the array,
	find the median of the element inside the window at each moving.
	(If there are even numbers in the array, return the N/2-th number after sorting the element in the window. )


	For array [1,2,7,8,5], moving window size k = 3. return [2,7,7]

	At first the window is at the start of the array like this

	[ | 1,2,7 | ,8,5] , return the median 2;

	then the window move one step forward.

	[1, | 2,7,8 | ,5], return the median 7;

	then the window move one step forward again.

	[1,2, | 7,8,5 | ], return the median 7;

####思路
- 很容易想到以下的方法,写的时候用的方法3,好写:(
- 方法1:暴力方法的话在k区间sort,时间复杂度 O(nklogk)
- 方法2: 在k区间找中位数,不就是find k th largest number in a array吗? 用quick select, 该操作O(k),然后指针向后,总时间复杂度O(nk)
- 方法3:使用heap记录两边的最大值最小值,同时指针向后移动 O(nk) , 因为default heap的删除操作时间复杂度是O(k)
- 方法4:使用hashheap,因为删除的操作时间复杂度缩小成为了O(logk),所以总时间复杂度O(nlogk) 就是hashheap有点难实现
- 方法5:使用Treemap,treemap也是sort,同时删除也是o(logk),总时间复杂度O(nlogk),面试可能会问treemap实现方法,对红黑树不熟悉就跪了(Treeset是不能有duplicate的,所以实现起来也有难度)

```java
public class Solution {
    /**
     * @param nums: A list of integers.
     * @return: The median of the element inside the window at each moving.
     */
    public ArrayList<Integer> medianSlidingWindow(int[] nums, int k) {
        // write your code here
        ArrayList<Integer> result = new ArrayList<Integer>();
        int size = nums.length;
        if (size == 0 || size < k) {
            return result;
        }

        PriorityQueue<Integer> minPQ = new PriorityQueue<Integer>();
        PriorityQueue<Integer> maxPQ = new PriorityQueue<Integer>(11, Collections.reverseOrder());

        int median = nums[0];
        int j = 0;
        if (k == 1) {
            result.add(median);
        }

        for (int i = 1; i < size; i++) {
            if (nums[i] > median) {
                minPQ.offer(nums[i]);
            } else {
                maxPQ.offer(nums[i]);
            }

            if (i > k - 1) {
                if (nums[j] > median) {
                    minPQ.remove(nums[j]);
                } else if (nums[j] < median) {
                    maxPQ.remove(nums[j]);
                } else {
                    median = Integer.MIN_VALUE;
                }
                j++;
            }

            if (median == Integer.MIN_VALUE) {
                median = minPQ.size() > maxPQ.size() ? minPQ.poll() : maxPQ.poll();
            } else {
                while (minPQ.size() >= maxPQ.size() + 2) {
                    maxPQ.offer(median);
                    median = minPQ.poll();
                }
                while (maxPQ.size() >= minPQ.size() + 1) {
                    minPQ.offer(median);
                    median = maxPQ.poll();
                }
            }
            if (i >= k - 1) {
                result.add(median);
            }
        }

        return result;
    }
}


```
