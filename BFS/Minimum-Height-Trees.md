##Minimum Height Trees

    Total Accepted: 10311 Total Submissions: 38708 Difficulty: Medium
    For a undirected graph with tree characteristics, we can choose any node as the root.
    The result graph is then a rooted tree.
    Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs).
    Given such a graph, write a function to find all the MHTs and return a list of their root labels.

    Format
    The graph contains n nodes which are labeled from 0 to n - 1.
    You will be given the number n and a list of undirected edges (each edge is a pair of labels).

    You can assume that no duplicate edges will appear in edges.
    Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

    Example 1:

    Given n = 4, edges = [[1, 0], [1, 2], [1, 3]]

            0
            |
            1
           / \
          2   3
    return [1]

    Example 2:

    Given n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

         0  1  2
          \ | /
            3
            |
            4
            |
            5
    return [3, 4]

    Show Hint
    Note:

    (1) According to the definition of tree on Wikipedia: “a tree is an undirected graph in
    which any two vertices are connected by exactly one path.
    In other words, any connected graph without simple cycles is a tree.”

    (2) The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.


####思路
- 最开始想的办法是,想把neighbor放好,然后用DFS找到最长的一条路线
- 然后找路线中中间值就可以
- 在input不大的时候可以使用
- 时间复杂度为O(n2)
- 但是如果有5000个Node,在递归中就会stack over flow了
- 参看第三个思路

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> result = new ArrayList<Integer>();
        if (edges == null || edges.length == 0) {
            return result;
        }

        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();

        for (int i = 0; i < edges.length; i++) {
            int first = edges[i][0];
            int second = edges[i][1];
            if (!map.containsKey(first)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(second);
                map.put(first, list);
            } else {
                map.get(first).add(second);
            }
            if (!map.containsKey(second)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(first);
                map.put(second, list);
            } else {
                map.get(second).add(first);
            }
        }

        List<List<Integer>> rootToLeafList = new ArrayList<List<Integer>>();
        List<Integer> list = new ArrayList<Integer>();
        boolean[] visited = new boolean[n];
        dfs(rootToLeafList, list, map, visited, 0);
        int maxLen = 0;

        for (int i = 0; i < rootToLeafList.size(); i++) {
            maxLen = Math.max(maxLen, rootToLeafList.get(i).size());
        }

        for (int i = 0; i < rootToLeafList.size(); i++) {
            List<Integer> cur = rootToLeafList.get(i);
            int len = cur.size();
            if (maxLen == len) {
                if (maxLen % 2 == 1) {
                    if (!result.contains(cur.get(len / 2))) {
                        result.add(cur.get(len / 2));
                    }
                } else {
                    if (!result.contains(cur.get(len / 2 - 1))) {
                        result.add(cur.get(len / 2 - 1));
                    }
                    if (!result.contains(cur.get(len / 2))) {
                        result.add(cur.get(len / 2));
                    }
                }
            }
        }

        return result;
    }

    public void dfs(List<List<Integer>> rootToLeafList, List<Integer> list, Map<Integer, List<Integer>> map, boolean[] visited, int node) {

        List<Integer> neighbor = map.get(node);
        boolean flag = true;
        for (int next : neighbor) {
            if (visited[next] == false) {
                flag = false;
                break;
            }
        }

        if (flag) {
            list.add(node);
            visited[node] = true;
            rootToLeafList.add(new ArrayList<Integer>(list));
            return;
        }

        visited[node] = true;
        for (int i = 0; i < neighbor.size(); i++) {
            int next = neighbor.get(i);
            if(!visited[next]) {
                list.add(node);
                dfs(rootToLeafList, list, map, visited, next);
                list.remove(list.size() - 1);
            }
        }
    }
}

```

####BFS
- O(n2)超时了

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        List<Integer> result = new ArrayList<Integer>();
        if (edges == null || edges.length == 0) {
            return result;
        }

        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();

        for (int i = 0; i < edges.length; i++) {
            int first = edges[i][0];
            int second = edges[i][1];
            if (!map.containsKey(first)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(second);
                map.put(first, list);
            } else {
                map.get(first).add(second);
            }
            if (!map.containsKey(second)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(first);
                map.put(second, list);
            } else {
                map.get(second).add(first);
            }
        }

        int[] candidate = new int[n];
        int minDepth = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            boolean[] visited = new boolean[n];
            Queue<Integer> queue = new LinkedList<Integer>();
            queue.offer(i);
            int depth = 0;
            while (!queue.isEmpty()) {
                int level = queue.size();
                for (int l = 0; l < level; l++) {
                    int cur = queue.poll();
                    visited[cur] = true;
                    List<Integer> neighbor = map.get(cur);
                    for (int j = 0; j < neighbor.size(); j++) {
                        int next = neighbor.get(j);
                        if (!visited[next]) {
                            queue.offer(next);
                            visited[next] = true;
                        }
                    }
                }
                depth++;
            }
            candidate[i] = depth;
            minDepth = Math.min(minDepth, depth);
        }

        for (int i = 0; i < n; i++) {
            if (candidate[i] == minDepth) {
                result.add(i);
            }
        }
        return result;
    }
}
```

####最优解
- [参考](http://www.elvisyu.com/minimum-height-trees/)
- 间接转化为了topological sort
- 从叶子出发,当做叶子外层到里层的direction,然后topological
- 只有当一个点 out degree = 1的时候,加入新的list以进行下一轮叶子遍历
- 最后可能剩一个节点,或者两个节点

```java
public class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        if (n == 1) return Collections.singletonList(0);
        Map<Integer, Set<Integer>> graph = new HashMap<Integer, Set<Integer>>();

        //create graph
        for (int[] edge : edges) {

            //put edge[1] into edge[0] neighbours
            if (graph.containsKey(edge[0])) {
                Set<Integer> neighbor = graph.get(edge[0]);
                neighbor.add(edge[1]);
            } else {
                Set<Integer> neighbor = new HashSet<Integer>();
                neighbor.add(edge[1]);
                graph.put(edge[0],neighbor);

            }

            //put edge[0] into edge[1] neighbours
            if (graph.containsKey(edge[1])) {
                Set<Integer> anotherneighbor = graph.get(edge[1]);
                anotherneighbor.add(edge[0]);
            } else {
                Set<Integer> anotherneighbor = new HashSet<Integer>();
                anotherneighbor.add(edge[0]);
                graph.put(edge[1],anotherneighbor);
            }
        }


        //In order to manipulate the graph map, I need to find leaves first,
        List<Integer> leaves = new ArrayList<Integer>();
        for (Map.Entry<Integer, Set<Integer>> node : graph.entrySet()) {
            if (node.getValue().size() == 1) {
                leaves.add(node.getKey());
            }
        }

        while (n > 2) {
            n -= leaves.size();
            List<Integer> newLeaves = new ArrayList<Integer>();

            for(Integer node : leaves) {
                //remove leaves
                Set<Integer> onlyNeigbour = graph.get(node);
                for(Integer onlyOne : onlyNeigbour) {
                    graph.get(onlyOne).remove(node);
                    if (graph.get(onlyOne).size() == 1) {
                        newLeaves.add(onlyOne);
                    }
                }
            }
            leaves = newLeaves;
        }
        return leaves;
    }

}
```
