##Route Between Two Nodes in Graph

35% Accepted

	Given a directed graph, design an algorithm to find out
	whether there is a route between two nodes.

	Have you met this question in a real interview? Yes
	Example
	Given graph:

	A----->B----->C
	 \     |
	  \    |
	   \   |
	    \  v
	     ->D----->E
	for s = B and t = E, return true

	for s = D and t = C, return false

####Tags Expand
- Cracking The Coding Interview
- Depth First Search
- Breadth First Search

####思路
- 典型BFS DFS

####BFS解法
```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<DirectedGraphNode>();
 *     }
 * };
 */
public class Solution {
   /**
     * @param graph: A list of Directed graph node
     * @param s: the starting Directed graph node
     * @param t: the terminal Directed graph node
     * @return: a boolean value
     */
    public boolean hasRoute(ArrayList<DirectedGraphNode> graph,
                            DirectedGraphNode s, DirectedGraphNode t) {
        // write your code here
        if (s == t) {
            return true;
        }
        if (graph == null || graph.size() == 0 || s == null || t == null) {
            return false;
        }
        Queue<DirectedGraphNode> queue = new LinkedList<DirectedGraphNode>();
        Set<DirectedGraphNode> hashset = new HashSet<DirectedGraphNode>();
        queue.offer(s);

        while (!queue.isEmpty()) {
            DirectedGraphNode cur = queue.poll();
            hashset.add(cur);
            if (cur == t) {
                return true;
            }
            for (DirectedGraphNode neighbor : cur.neighbors) {
                if (hashset.contains(neighbor)) {
                    continue;
                }
                queue.offer(neighbor);
            }
        }

        // hashset.clear();
        // queue.offer(t);
        // while (!queue.isEmpty()) {
        //     DirectedGraphNode cur = queue.poll();
        //     hashset.add(cur);
        //     if (cur == s) {
        //         return true;
        //     }
        //     for (DirectedGraphNode neighbor : cur.neighbors) {
        //         if (hashset.contains(neighbor)) {
        //             continue;
        //         }
        //         queue.offer(neighbor);
        //     }
        // }

        return false;
    }

}

```

####DFS解法

```java
/**
 * Definition for Directed graph.
 * class DirectedGraphNode {
 *     int label;
 *     ArrayList<DirectedGraphNode> neighbors;
 *     DirectedGraphNode(int x) {
 *         label = x;
 *         neighbors = new ArrayList<DirectedGraphNode>();
 *     }
 * };
 */
public class Solution {
   /**
     * @param graph: A list of Directed graph node
     * @param s: the starting Directed graph node
     * @param t: the terminal Directed graph node
     * @return: a boolean value
     */
    public boolean hasRoute(ArrayList<DirectedGraphNode> graph,
                            DirectedGraphNode s, DirectedGraphNode t) {
        // write your code here
        return dfs(s, t);
    }

    public boolean dfs(DirectedGraphNode s, DirectedGraphNode t) {
        if (s == t) {
            return true;
        }

        if (s.neighbors.size() == 0) {
            return false;
        }

        boolean result = false;

        for (DirectedGraphNode neighbor : s.neighbors) {
            result = result || dfs(neighbor, t);
        }

        return result;
    }
}
```
