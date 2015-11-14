# Heap - 堆

一般情况下，堆通常指的是**二叉堆**，**二叉堆**是一个近似**完全二叉树**的数据结构，**即披着二叉树羊皮的数组，**故使用数组来实现较为便利。子结点的键值或索引总是小于（或者大于）它的父节点，且每个节点的左右子树又是一个**二叉堆**(大根堆或者小根堆)。根节点最大的堆叫做最大堆或大根堆，根节点最小的堆叫做最小堆或小根堆。**常被用作实现优先队列。**


![Heap Complexity](../image/heap.png)

##Priority Queue
[Java PriorityQueue Class Example](http://www.programcreek.com/2009/02/using-the-priorityqueue-class-example/)
- PriorityQueue provides O(log(n)) time for the enqueing and dequeing methods (offer, poll, remove() and add); linear time for the remove(Object) and contains(Object) methods

```java
import java.util.Comparator;
import java.util.PriorityQueue;

public class PriorityQueueTest {

	static class PQsort implements Comparator<Integer> {

		public int compare(Integer one, Integer two) {
			return two - one;
		}
	}

	public static void main(String[] args) {
		int[] ia = { 1, 10, 5, 3, 4, 7, 6, 9, 8 };
		PriorityQueue<Integer> pq1 = new PriorityQueue<Integer>();

		// use offer() method to add elements to the PriorityQueue pq1
		for (int x : ia) {
			pq1.offer(x);
		}

		System.out.println("pq1: " + pq1);

		PQsort pqs = new PQsort();
		PriorityQueue<Integer> pq2 = new PriorityQueue<Integer>(10, pqs);
		// In this particular case, we can simply use Collections.reverseOrder()
		// instead of self-defined comparator
		for (int x : ia) {
			pq2.offer(x);
		}

		System.out.println("pq2: " + pq2);

		// print size
		System.out.println("size: " + pq2.size());
		// return highest priority element in the queue without removing it
		System.out.println("peek: " + pq2.peek());
		// print size
		System.out.println("size: " + pq2.size());
		// return highest priority element and removes it from the queue
		System.out.println("poll: " + pq2.poll());
		// print size
		System.out.println("size: " + pq2.size());

		System.out.print("pq2: " + pq2);

	}
}
```

Output:

```
	pq1: [1, 3, 5, 8, 4, 7, 6, 10, 9]
	pq2: [10, 9, 7, 8, 3, 5, 6, 1, 4]
	size: 9
	peek: 10
	size: 9
	poll: 10
	size: 8
	pq2: [9, 8, 7, 4, 3, 5, 6, 1]
```

## 特点

1. **以数组表示，但是以完全二叉树的方式理解**。
2. 唯一能够同时最优地利用空间和时间的方法——最坏情况下也能保证使用 $$2N \log N$$ 次比较和恒定的额外空间。
3. 在索引从0开始的数组中：
  - 父节点 `i` 的左子节点在位置`(2*i+1)`
  - 父节点 `i` 的右子节点在位置`(2*i+2)`
  - 子节点 `i` 的父节点在位置`floor((i-1)/2)`

## 堆的操作
- 取一个数 时间复杂度O(logn)
- sift down/up



## 堆的常用方式

以大根堆为例，堆的常用操作如下。

1. 最大堆调整（Max_Heapify）：将堆的末端子节点作调整，使得子节点永远小于父节点
2. 创建最大堆（Build_Max_Heap）：将堆所有数据重新排序
3. 堆排序（HeapSort）：移除位在第一个数据的根节点，并做最大堆调整的递归运算

其中步骤1是给步骤2和3用的。

- 得到/删除最大值是针对已经实现了最大/最小堆说的，已经heapify了，所以针对一个元素sift sink就行
- 而heapify的时候，这个时候是乱序的，需要从底层开始不断sink，一层一层往上走（得到值后，又跟下层进行对比）

![Heapsort-example](../image/Heapsort-example.gif)
