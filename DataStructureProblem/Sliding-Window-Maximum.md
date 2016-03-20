##Sliding Window Maximum
	Total Accepted: 22812 Total Submissions: 85476 Difficulty: Hard
	Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

	For example,
	Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.

	Window position                Max
	---------------               -----
	[1  3  -1] -3  5  3  6  7       3
	 1 [3  -1  -3] 5  3  6  7       3
	 1  3 [-1  -3  5] 3  6  7       5
	 1  3  -1 [-3  5  3] 6  7       5
	 1  3  -1  -3 [5  3  6] 7       6
	 1  3  -1  -3  5 [3  6  7]      7
	Therefore, return the max sliding window as [3,3,5,5,6,7].

	Note:
	You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

	Follow up:
	Could you solve it in linear time?

####思路
- 思路1:max heap去求最大,然后指针不断往前走,因为heap删除操作O(k),所以总时间复杂度为O(nk),为下面代码第一个实现
- 思路2:max hashheap求最大,因为hashheap删除操作O(logk),所以总时间复杂度为O(nlogk)
- 思路3:使用deque,deque首处就是最大值所在处,如果后面加入的元素更大,就从之前后面poll出去,如果长度超过了k,就把deque首处元素poll出去. 关键之处在于使用deque储存的是Index,而不是元素值本身. 时间复杂度O(n),为下面代码第二个实现

####heap实现
```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {

        int size = nums.length;

        if (size == 0 || k == 0 || size < k) {
            return new int[0];
        }

        int[] result = new int[size - k + 1];
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>(k, Collections.reverseOrder());

        for (int x = 0; x < k; x++) {
            pq.offer(nums[x]);
        }

        int i = 0;
        int j = k;
        while (j < size) {
            result[i] = pq.peek();
            pq.remove(nums[i++]);
            pq.offer(nums[j++]);
        }
        result[i] = pq.peek();


        return result;
    }
}
```

####deque实现
```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {

        int size = nums.length;

        if (size == 0 || k == 0 || size < k) {
            return new int[0];
        }
        int[] result = new int[size - k + 1];

        Deque<Integer> deque = new LinkedList<Integer>();
        deque.offer(0);
        int i = 0;
        for (i = 1; i < k; i++) {
            while (!deque.isEmpty() && nums[i] >= nums[deque.getLast()]) {
                deque.removeLast();
            }
            deque.offer(i);
        }

        int index = 0;
        result[index++] = nums[deque.getFirst()];

        while (i < size) {
            if (i - deque.getFirst() >= k) {
                deque.removeFirst();
            }
            while (!deque.isEmpty() && nums[i] >= nums[deque.getLast()]) {
                deque.removeLast();
            }
            deque.offer(i);
            i++;
            result[index++] = nums[deque.getFirst()];
        }

        return result;
    }
}
```
