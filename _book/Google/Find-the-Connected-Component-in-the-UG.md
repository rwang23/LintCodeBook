##Find the Connected Component in the Undirected Graph

18% Accepted

	Find the number connected component in the undirected graph.
	Each node in the graph contains a label and a list of its neighbors.
	(a connected component (or just component) of an undirected graph is a subgraph
	in which any two vertices are connected to each other by paths,
	and which is connected to no additional vertices in the supergraph.)

	Have you met this question in a real interview? Yes
	Example
	Given graph:

	A------B  C
	 \     |  |
	  \    |  |
	   \   |  |
	    \  |  |
	      D   E
	Return {A,B,D}, {C,E}. Since there are two connected component which is {A,B,D}, {C,E}

####Tags Expand
- Breadth First Search

```java
/**
 * Definition for Undirected graph.
 * class UndirectedGraphNode {
 *     int label;
 *     ArrayList<UndirectedGraphNode> neighbors;
 *     UndirectedGraphNode(int x) { label = x; neighbors = new ArrayList<UndirectedGraphNode>(); }
 * };
 */
public class Solution {
    /**
     * @param nodes a array of Undirected graph node
     * @return a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(ArrayList<UndirectedGraphNode> nodes) {
        // Write your code here
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        HashMap<UndirectedGraphNode, Boolean> hashmap = new HashMap<UndirectedGraphNode, Boolean>();

        for (UndirectedGraphNode node : nodes) {
            if (hashmap.containsKey(node)) {
                continue;
            }
            List<Integer> list = new ArrayList<Integer>();
            Queue<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
            list.add(node.label);
            queue.offer(node);
            hashmap.put(node, true);

            while (!queue.isEmpty()) {
                UndirectedGraphNode cur = queue.poll();
                for (UndirectedGraphNode neighbor : cur.neighbors) {
                    if (!hashmap.containsKey(neighbor)) {
                        queue.offer(neighbor);
                        hashmap.put(neighbor, true);
                        list.add(neighbor.label);
                    }
                }
            }
            Collections.sort(list);
            result.add(new ArrayList(list));
        }

        return result;
    }
}

```
