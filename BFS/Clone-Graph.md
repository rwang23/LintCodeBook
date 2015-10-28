##Clone Graph

26% Accepted

	Clone an undirected graph. Each node in the graph contains a label and a list of its neighbors.
	OJ's undirected graph serialization:
	Nodes are labeled uniquely.

	We use # as a separator for each node, and , as a separator for node label and each neighbor of the node.
	As an example, consider the serialized graph {0,1,2#1,2#2,2}.

	The graph has a total of three nodes, and therefore contains three parts as separated by #.

	First node is labeled as 0. Connect node 0 to both nodes 1 and 2.
	Second node is labeled as 1. Connect node 1 to node 2.
	Third node is labeled as 2. Connect node 2 to node 2 (itself), thus forming a self-cycle.
	Visually, the graph looks like the following:

       1
      / \
     /   \
    0 --- 2
         / \
         \_/

####思路
- BFS = Queue + HashMap
- Queue是abstract 所以 Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
- 这道题是深拷贝，深拷贝的意思就是单独再复制出来，新的跟旧的在内存地址上没有关联

```java
/**
 * Definition for undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        // write your code here
        if (node == null) {
            return node;
        }
        Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
        HashMap<UndirectedGraphNode, UndirectedGraphNode> hashmap = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
        queue.offer(node);
        UndirectedGraphNode newHead = new UndirectedGraphNode(node.label);
        hashmap.put(node, newHead);

        while (!queue.isEmpty()) {

            UndirectedGraphNode cur = queue.poll();
            UndirectedGraphNode curinhash = hashmap.get(cur);
            int length = cur.neighbors.size();

            for (int i = 0; i < length; i++) {
                UndirectedGraphNode next = cur.neighbors.get(i);
                /*
                这里必须使用 copy = new UndirectedGraphNode(next.label)
                不能够将next直接用 不能将next 加进neighbor，因为我的是新的节点，不能跟原来的节点扯上关系
                这里很容易错误
                如果HashMap不包含，就在neighbor加入copy,如果不包含，说明遍历过了，有可能这个点已经加入了neighbor,所以我么你直接使用，把整个加入到neighbor
                 */
                UndirectedGraphNode copy = new UndirectedGraphNode(next.label);
                if (!hashmap.containsKey(next)) {
                    queue.offer(next);
                    hashmap.put(next, copy);
                    curinhash.neighbors.add(copy);
                } else {
                    curinhash.neighbors.add(hashmap.get(next));
                }
            }
            hashmap.put(cur, curinhash);
        }
        return newHead;
    }
}

```
