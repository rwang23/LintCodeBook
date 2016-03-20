##Find Median from Data Stream
Total Accepted: 12907 Total Submissions: 59190 Difficulty: Hard
Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples:
[2,3,4] , the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Design a data structure that supports the following two operations:

void addNum(int num) - Add a integer number from the data stream to the data structure.
double findMedian() - Return the median of all elements so far.
For example:

add(1)
add(2)
findMedian() -> 1.5
add(3)
findMedian() -> 2


####思路
- 加入数据选在加在中位数左边或者右边,维持左边的maxPQ,右边minPQ
- 维持右边的size一定大于左边,但是最多不超过一个


```java
class MedianFinder {

    private PriorityQueue<Integer> maxPQ = new PriorityQueue<Integer>(11, Collections.reverseOrder());
    private PriorityQueue<Integer> minPQ = new PriorityQueue<Integer>(11);
    private int median = 0;
    private int size = 0;

    // Adds a number into the data structure.
    public void addNum(int num) {
        if (size == 0) {
            median = num;
            size++;
            return;
        }

        if (num >= median) {
            minPQ.offer(num);
        } else {
            maxPQ.offer(num);
        }

        size++;

        while (minPQ.size() >= maxPQ.size() + 2) {
            maxPQ.offer(median);
            median = minPQ.poll();
        }

        while (maxPQ.size() > minPQ.size()) {
            minPQ.offer(median);
            median = maxPQ.poll();
        }


    }

    // Returns the median of current data stream
    public double findMedian() {
        return (size % 2 == 1) ? median : (median + minPQ.peek()) / 2.0;
    }
};

// Your MedianFinder object will be instantiated and called as such:
// MedianFinder mf = new MedianFinder();
// mf.addNum(1);
// mf.findMedian();
```
