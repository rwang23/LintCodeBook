##Heapify

31% Accepted

	Given an integer array, heapify it into a min-heap array.

	For a heap array A, A[0] is the root of heap, and for each A[i], A[i * 2 + 1] is the left child of A[i] and A[i * 2 + 2] is the right child of A[i].
	Have you met this question in a real interview? Yes
	Example
	Given [3,2,1,4,5], return [1,2,3,4,5] or any legal heap array.

####Challenge
- O(n) time complexity

####Clarification
	What is heap?

	Heap is a data structure, which usually have three methods: push, pop and top. where "push" add a new element the heap, "pop" delete the minimum/maximum element in the heap, "top" return the minimum/maximum element.

	What is heapify?
	Convert an unordered integer array into a heap array. If it is min-heap, for each element A[i],
	we will get A[i * 2 + 1] >= A[i] and A[i * 2 + 2] >= A[i].


####Tags Expand
- LintCode Copyright Heap

####思路
- Heap采用自底向上的方法
- [Heap Youtube Video](https://www.youtube.com/watch?v=d3qd_wQdYqg)
- 首先把head想做树，如果从下往上数（倒数）第h层的所有点已经是heapified的了，
- 那么让倒数第h+1层的一个点heapify所需要的操作数最多是h步（最坏情况，最小堆里这个数是最大的，
- 所以需要把它一层一层往下转移直到最底层）。所以对每一个h+1层的点（node）来说，复杂度O(h)。
- h+1层有这么多点：n/2^(k+1)，所以总得复杂度就是O(h) * (n/2^(k+1)) 再对所有层数求和。最终结果就是个O(n)的。


```java
public class Solution {
    /**
     * @param A: Given an integer array
     * @return: void
     */
    private void siftdown(int[] A, int k) {
        while (k < A.length) {
            int smallest = k;
            if (k * 2 + 1 < A.length && A[k * 2 + 1] < A[smallest]) {
                smallest = k * 2 + 1;
            }
            if (k * 2 + 2 < A.length && A[k * 2 + 2] < A[smallest]) {
                smallest = k * 2 + 2;
            }
            if (smallest == k) {
                break;
            }
            int temp = A[smallest];
            A[smallest] = A[k];
            A[k] = temp;

            k = smallest;
        }
    }

    public void heapify(int[] A) {
        for (int i = A.length / 2; i >= 0; i--) {
            siftdown(A, i);
        } // for
    }
}
```
