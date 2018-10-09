# Queue - 队列

Queue 是一个 FIFO（先进先出）的数据结构，并发中使用较多，可以安全地将对象从一个任务传给另一个任务。

## 编程实现

### Java

Queue 在 Java 中是 Interface, 一种实现是 LinkedList, LinkedList 向上转型为 Queue, Queue 通常不能存储 `null` 元素，否则与 `poll()` 等方法的返回值混淆。

```
Queue<Integer> q = new LinkedList<Integer>();
int qLen = q.size(); // get queue length
```

###Java常用的队列包括如下几种：

队列内部存储元素的方式，一般有两种，数组（array）和链表（linked list）。两者的最主要区别是：
数组对随机访问有较好性能。
链表对插入和删除元素有较好性能。

- ArrayDeque：数组存储。实现Deque接口，而Deque是Queue接口的子接口，代表双端队列（double-ended queue）。
- LinkedList：链表存储。实现List接口和Duque接口，不仅可做队列，还可以作为双端队列，或栈（stack）来使用。

#### Methods

| 0:0 | Throws exception | Returns special value |
| -- | -- | -- |
| Insert | add(e) | offer(e) |
| Remove | remove() | poll() |
| Examine | element() | peek() |

优先考虑右侧方法，右侧元素不存在时返回 `null`. 判断非空时使用`isEmpty()`方法，继承自 Collection.

#### 用法
- 常用在树的遍历里边

## Priority Queue - 优先队列

应用程序常常需要处理带有优先级的业务，优先级最高的业务首先得到服务。因此优先队列这种数据结构应运而生。优先队列中的每个元素都有各自的优先级，优先级最高的元素最先得到服务；优先级相同的元素按照其在优先队列中的顺序得到服务。

优先队列可以使用数组或链表实现，从时间和空间复杂度来说，往往用二叉堆来实现。

### Java

Java 中提供`PriorityQueue`类，该类是 Interface Queue 的另外一种实现，和`LinkedList`的区别主要在于排序行为而不是性能，基于 priority heap 实现，非`synchronized`，故多线程下应使用`PriorityBlockingQueue`. 默认为自然序（小根堆），需要其他排序方式可自行实现`Comparator`接口，选用合适的构造器初始化。使用迭代器遍历时不保证有序，有序访问时需要使用`Arrays.sort(pq.toArray())`.

不同方法的时间复杂度：

- enqueuing and dequeuing: `offer`, `poll`, `remove()` and `add` - O(\log n)
- Object: `remove(Object)` and `contains(Object)` - O(n)
- 自己实现的heap如果加上hashmap,可以实现remove O(logn) contains O(1)
- retrieval: `peek`, `element`, and `size` - O(1).

###一些用法
- PriorityQueue(): Creates a PriorityQueue with the default initial capacity (11) that orders its elements according to their natural ordering.
- 默认是最小heap，每次出的话，得到最小值
- 最大heap使用reverseOrder
- PriorityQueue<Integer> queue = new PriorityQueue<>(10, Collections.reverseOrder());

## Deque - 双端队列

双端队列（deque，全名double-ended queue）可以让你在任何一端添加或者移除元素，因此它是一种具有队列和栈性质的数据结构。

### Java

Java 在1.6之后提供了 Deque 接口，既可使用`ArrayDeque`（数组）来实现，也可以使用`LinkedList`（链表）来实现。前者是一个数组外加首尾索引，后者是双向链表。
```
  Java常用的队列包括如下几种：
  ArrayDeque：数组存储。实现Deque接口，而Deque是Queue接口的子接口，代表双端队列（double-ended queue）。
  LinkedList：链表存储。实现List接口和Duque接口，不仅可做队列，还可以作为双端队列，或栈（stack）来使用。
  C++中，使用<queue>中的queue模板类，模板需两个参数，元素类型和容器类型，元素类型必要，而容器类型可选，默认deque，可改用list（链表）类型。
  Python中，使用collections.deque，双端队列。
```
```
Deque<Integer> deque = new ArrayDeque<Integer>();
```

###Message queue
- 常用的消息队列实现包括RabbitMQ，ZeroMQ, Kafka等等。
[为什么要用消息队列](http://www.ywnds.com/?p=5791)
[RabbitMQ 应用及原理](https://blog.csdn.net/whoamiyang/article/details/54954780)
#### Methods

<table>
  <tr>
    <td></td>
    <td colspan="2">First Element (Head)</td>
    <td colspan="2">Last Element (Tail)</td>
  </tr>
  <tr>
    <td></td>
    <td>Throws exception</td>
    <td>Special value</td>
    <td>Throws exception</td>
    <td>Special value</td>
  </tr>
  <tr>
    <td>Insert</td>
    <td>addFirst(e)</td>
    <td>offerFirst(e)</td>
    <td>addLast(e)</td>
    <td>offerLast(e)</td>
  </tr>
  <tr>
    <td>Remove</td>
    <td>removeFirst()</td>
    <td>pollFirst()</td>
    <td>removeLast()</td>
    <td>pollLast()</td>
  </tr>
  <tr>
    <td>Examine</td>
    <td>getFirst()</td>
    <td>peekFirst()</td>
    <td>getLast()</td>
    <td>peekLast()</td>
  </tr>
</table>

其中`offerLast`和 Queue 中的`offer`功能相同，都是从尾部插入。

## Reference

- [优先队列 - 维基百科，自由的百科全书](http://zh.wikipedia.org/zh/%E5%84%AA%E5%85%88%E4%BD%87%E5%88%97)
- [双端队列 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%8F%8C%E7%AB%AF%E9%98%9F%E5%88%97)
