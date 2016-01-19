Merge k Sorted Arrays

	Given k sorted integer arrays, merge them into one sorted array.

	Have you met this question in a real interview? Yes
	Example
	Given 3 sorted arrays:

	[
	  [1, 3, 5, 7],
	  [2, 4, 6],
	  [0, 8, 9, 10, 11]
	]
	return [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11].

####Challenge
Do it in O(N log k).

N is the total number of integers.
k is the number of arrays.

####Tags Expand
Heap Priority Queue

####思路
- 第一种想到的方法是Merge Sort, 但是Merge sort的时间复杂度是 nklognk 时间较长
- 因为Merge sort要么需要n多的辅助数组去实现两两排序,要么就把所有元素移到一个数组中,这样长度就变成了nk
- 第二种方法就利用到了priority queue/ heap
- 写出来comparator来排序,同时因为需要知道每个元素的位置,所以创造了一个element类
- 最开始只保存每一个数列的第一个数(因为已经排好序,所以是分别的每个数列最小值),这样在heap中就有了最小值
- 然后poll出最小值,把该数列的第二数加进来继续比较

```java
public class Solution {
    /**
     * @param arrays k sorted integer arrays
     * @return a sorted array
     */
    class Element {
        int row;
        int col;
        int val;
        Element(int val, int col, int row) {
            this.val = val;
            this.col = col;
            this.row = row;
        }
    }

    private Comparator<Element> pqcomparator = new Comparator<Element>() {
        public int compare(Element e1, Element e2) {
            return e1.val - e2.val;
        }
    };

    public List<Integer> mergekSortedArrays(int[][] arrays) {
        // Write your code here
        if (arrays == null) {
            return new ArrayList<Integer>();
        }

        int size = arrays.length;
        PriorityQueue<Element> pq = new PriorityQueue<Element>(size, pqcomparator);

        for (int i = 0; i < size; i++) {
            if (arrays[i].length > 0) {
                Element cur = new Element(arrays[i][0], 0, i);
                pq.offer(cur);
            }
        }

        List<Integer> result = new ArrayList<Integer>();

        while (!pq.isEmpty()) {
            Element cur = pq.poll();
            result.add(cur.val);
            if (cur.col + 1 < arrays[cur.row].length) {
                Element next = new Element(arrays[cur.row][cur.col + 1], cur.col + 1, cur.row);
                pq.offer(next);
            }
        }
        return result;
    }
}
```
