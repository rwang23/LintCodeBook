##Topological Sorting

25% Accepted

    Given an directed graph, a topological order of the graph nodes is defined as follow:

    For each directed edge A -> B in graph, A must before B in the order list.
    The first node in the order can be any node in the graph with no nodes direct to it.
    Find any topological order for the given graph.

    For graph as follow:

![](../image/topologicalsort.jpeg)

         The topological order can be:

         [0, 1, 2, 3, 4, 5]
         [0, 2, 3, 1, 5, 4]

####Note
You can assume that there is at least one topological order in the graph.

####Challenge
Can you do it in both BFS and DFS?

####Tags Expand
- LintCode Copyright
- Geeks for Geeks
- DFS
- BFS

####思路
- BFS方法

####一刷
```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
 public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // write your code here
        ArrayList<DirectedGraphNode> result = new ArrayList<DirectedGraphNode>();
        HashMap<DirectedGraphNode, Integer> map = new HashMap();
        /*
        先进行入度计算，用的哈希表储存
         */
        for (DirectedGraphNode node : graph) {
            for (DirectedGraphNode neighbor : node.neighbors) {
                if (map.containsKey(neighbor)) {
                    map.put(neighbor, map.get(neighbor) + 1);
                } else {
                    map.put(neighbor, 1);
                }
            }
        }
        /*
        然后找到根节点(入度为0)
         */
        Queue<DirectedGraphNode> q = new LinkedList<DirectedGraphNode>();
        for (DirectedGraphNode node : graph) {
            if (!map.containsKey(node)) {
                q.offer(node);
                result.add(node);
            }
        }
        /*
         对图遍历，每次遇到节点，该节点入度减一，当入度为0时，说明前面的遍历完了
         */
        while (!q.isEmpty()) {
            DirectedGraphNode node = q.poll();
            for (DirectedGraphNode n : node.neighbors) {
                map.put(n, map.get(n) - 1);
                if (map.get(n) == 0) {
                    result.add(n);
                    q.offer(n);
                }
            }
        }
        return result;
    }
}
```
####二刷
- 引入了count，最后比较results和count的大小，这样可以避免如果在图中出现了环的情况，那么其实就无解

```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) { label = x; neighbors = new ArrayList<DirectedGraphNode>(); }
 * };
 */

public class Solution {
    /*
     * @param graph: A list of Directed graph node
     * @return: Any topological order for the given graph.
     */
    public ArrayList<DirectedGraphNode> topSort(ArrayList<DirectedGraphNode> graph) {
        // write your code here
        if (graph == null) {
            return graph;
        }
        
        Map<DirectedGraphNode, Integer> indegrees = new HashMap<DirectedGraphNode, Integer>();
        
        for (DirectedGraphNode node : graph) {
            indegrees.put(node, 0);
        }
        
        int count = 0;
        for (DirectedGraphNode node : graph) { 
            for (DirectedGraphNode neighbor : node.neighbors) {
                int indegree = indegrees.get(neighbor);
                indegrees.put(neighbor, indegree + 1);
            }
            count++;
        }
        
        Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
        ArrayList<DirectedGraphNode> results = new ArrayList<DirectedGraphNode>();

        for (Map.Entry<DirectedGraphNode, Integer> entry : indegrees.entrySet()) {
            DirectedGraphNode node = entry.getKey();
            int indegree = entry.getValue();
            if (indegree == 0) {
                queue.offer(node);
            }
        }
        
        while (!queue.isEmpty()) {
            DirectedGraphNode cur = queue.poll();
            results.add(cur);
            
            for (DirectedGraphNode neighbor : cur.neighbors) {

                int indegree = indegrees.get(neighbor) - 1;
                indegrees.put(neighbor, indegree);
                if (indegree == 0) {
                    queue.offer(neighbor);
                }
            }
        }
        
        if (results.size() != count) {
            return new ArrayList<DirectedGraphNode>();
        }
        return results;
    }
}
```
####DFS方法
- 跟BFS一样
- 先找indegree
- 在对indegree == 0 的点,去进行DFS,DFS过程中,对该点的neighbor indegree减1,如果neighbor indegree = 0,那么递归这个点
