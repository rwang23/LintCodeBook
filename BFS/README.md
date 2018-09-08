##BFS(下半部分是拓扑排序)

- Queue + HashMap -> BFS
- 从图上一个点走到其他所有点
- 在图上计算两点之间的最短距离

更细一点的划分的话，这一类的问题还可以分为：
```
层级遍历 Level Order Traversal
由点及面 Connected Component
拓扑排序 Topological Sorting
```
##图（引用九章说明）

有很多种方法可以存储一个图，最常用的莫过于：
- 邻接矩阵
- 邻接表

而邻接矩阵因为耗费空间过大，我们通常在工程中都是使用邻接表作为图的存储结构。

###邻接矩阵
```
邻接矩阵 Adjacent Matrix

[
  [1,0,0,1],
  [0,1,1,0],
  [0,1,1,0],
  [1,0,0,1]
]
```
```
例如上图表示0号点和3号点有连边。1号点和2号店有连边。
当然，每个点和自己也是默认有连边的。
图中的 0 表示不连通，1 表示连通。
我们也可以用一个更具体的整数值来表示连边的长度。
邻接矩阵我们可以直接用一个二维数组表示，如int[][] matrix;。
这种数据结构因为耗费 O(n^2) 的空间，所以在稀疏图上浪费很大，因此并不常用。
```
###邻接表
```
邻接表 (Adjacent List)

[
  [1],
  [0,2,3],
  [1],
  [1]
]
```
```
这个图表示 0 和 1 之间有连边，1 和 2 之间有连边，1 和 3 之间有连边。
即每个点上存储自己有哪些邻居（有哪些连通的点）。
这种方式下，空间耗费和边数成正比，
可以记做 O(m)，m代表边数。m最坏情况下虽然也是 O(n^2)，
但是邻接表的存储方式大部分情况下会比邻接矩阵更省空间。
```

```
可以用自定义的类来实现邻接表

class DirectedGraphNode {
    int label;
    List<DirectedGraphNode> neighbors;
    ...
}

也可以用也可以使用 HashMap 和 HashSet 搭配的方式来存储邻接表

Map<T, Set<T>> = new HashMap<Integer, HashSet<Integer>>();
```

##拓扑排序
- 在图论中，由一个有向无环图的顶点组成的序列，当且仅当满足下列条件时，称为该图的一个拓扑排序（英语：Topological sorting）。
- 每个顶点出现且只出现一次；
- 若A在序列中排在B的前面，则在图中不存在从B到A的路径。
- 也可以定义为：拓扑排序是对有向无环图的顶点的一种排序，它使得如果存在一条从顶点A到顶点B的路径，那么在排序中B出现在A的后面

###实际运用
- 拓扑排序 Topological Sorting 是一个经典的图论问题。他实际的运用中，拓扑排序可以做如下的一些事情：
- 检测编译时的循环依赖
- 制定有依赖关系的任务的执行顺序
- 一张图的拓扑序列可以有很多个，也可能没有。拓扑排序只需要找到其中一个序列，无需找到所有序列。

###算法
- 计算所有出度，找出入度为0的，加入宽度有限搜索队列的queue里
- 找出入度为0这些点的出口，减去1的入度，再把入读为0的加入queue
- 直至队列为空

```java
Queue<T> queue = new LinkedList<>();
Set<T> set = new HashSet<>();

set.add(start);
queue.offer(start);
while (!queue.isEmpty()) {
//添加了这个size就是分层遍历的宽搜，不然就是不分层
    int size = queue.size();
    for (int i = 0; i < size; i++) {
        T head = queue.poll();
        for (T neighbor : head.neighbors) {
            if (!set.contains(neighbor)) {
                set.add(neighbor);
                queue.offer(neighbor);
            }
        }
    }
}
```
###双向宽度优先搜索算法(九章)
BFS的优化办法就是Bidirectional BFS

####算法描述
- 双向宽度优先搜索本质上还是BFS，只不过变成了起点向终点和终点向起点同时进行扩展，直至两个方向上出现同一个子节点，搜索结束。
- 我们还是可以利用队列来实现：一个队列保存从起点开始搜索的状态，另一个保存从终点开始的状态，两边如果相交了，那么搜索结束。
- 起点到终点的最短距离即为起点到相交节点的距离与终点到相交节点的距离之和。

####双向BFS是否真的能提高效率？
```
假设单向BFS需要搜索 N 层才能到达终点，每层的判断量为 X，那么总的运算量为 X ^ NX 
N
 . 如果换成是双向BFS，前后各自需要搜索 N / 2 层，总运算量为 2 * X ^ {N / 2}2∗X 
N/2
 。如果 N 比较大且X 不为 1，则运算量相较于单向BFS可以大大减少，差不多可以减少到原来规模的根号的量级。
 ```
 
 ```java
 /**
 * Definition for graph node.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { 
 *         label = x; neighbors = new ArrayList<UndirectedGraphNode>(); 
 *     }
 * };
 */
public int doubleBFS(UndirectedGraphNode start, UndirectedGraphNode end) {
    if (start.equals(end)) {
        return 1;
    }
    // 起点开始的BFS队列
    Queue<UndirectedGraphNode> startQueue = new LinkedList<>();
    // 终点开始的BFS队列
    Queue<UndirectedGraphNode> endQueue = new LinkedList<>();
    startQueue.add(start);
    endQueue.add(end);
    int step = 0;
    // 记录从起点开始访问到的节点
    Set<UndirectedGraphNode> startVisited = new HashSet<>();
    // 记录从终点开始访问到的节点
    Set<UndirectedGraphNode> endVisited = new HashSet<>();
    startVisited.add(start);
    endVisited.add(end);
    while (!startQueue.isEmpty() || !endQueue.isEmpty()) {
        int startSize = startQueue.size();
        int endSize = endQueue.size();
        // 按层遍历
        step ++;
        for (int i = 0; i < startSize; i ++) {
            UndirectedGraphNode cur = startQueue.poll();
            for (UndirectedGraphNode neighbor : cur.neighbors) {
                if (startVisited.contains(neighbor)) {//重复节点
                    continue;
                } else if (endVisited.contains(neighbor)) {//相交
                    return step;
                } else {
                    startVisited.add(neighbor);
                    startQueue.add(neighbor);
                }
            }
        }
        step ++;
        for (int i = 0; i < endSize; i ++) {
            UndirectedGraphNode cur = endQueue.poll();
            for (UndirectedGraphNode neighbor : cur.neighbors) {
                if (endVisited.contains(neighbor)) {
                    continue;
                } else if (startVisited.contains(neighbor)) {
                    return step;
                } else {
                    endVisited.add(neighbor);
                    endQueue.add(neighbor);
                }
            }
        }    
    }
    return -1; // 不连通
}
 ```
