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
- [参考](https://leetcode.com/discuss/72739/two-o-n-solutions)

####BFS找最长的path
- [参考](https://github.com/lydxlx1/LeetCode/blob/master/src/_310.java)
- 非常棒的BFS解法
- 先随便找一个点找到这个点的最长path,当前最长path的终点一定就是整个图最长path的一个起始点或者结束点
- 选着这个起始点,再继续找最长path,这条最长path就是整个图最长path
- 就是一直没想明白如何把节点的顺序记录下来,从而把最长path记录下来
- 这个解法很棒,用了两个数组
- 用了一个数组来存当前的点离起点的距离,一个数组利用了我们只有label 0 -> n-1,所以利用了整数的性质,记录下来的当前节点的prev节点(也是一个整数表示)
- 这样找完之后,我们就能通过prev这个数组找到整个最长path的所有节点,再加入到arraylist里边,直接可以找重点了

```
    It is easy to see that the root of an MHT has to be the middle point (or two middle points) of the longest path of the tree.
    Though multiple longest paths can appear in an unrooted tree, they must share the same middle point(s).

    Computing the longest path of a unrooted tree can be done, in O(n) time, by tree dp, or simply 2 tree traversals (dfs or bfs).
    The following code does the latter.

    Randomly select a node x as the root, do a dfs/bfs to find the node y that has the longest distance from y.
    Then y must be one of the endpoints on some longest path.
    Let y the new root, and do another dfs/bfs. Find the node z that has the longest distance from y.
    Now, the path from y to z is the longest one, and thus its middle point(s) is the answer.
```

```java
public class Solution {
    int n;
    List<Integer>[] e;

    private void bfs(int start, int[] dist, int[] pre) {
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new ArrayDeque<>();
        queue.add(start);
        dist[start] = 0;
        visited[start] = true;
        pre[start] = -1;
        while (!queue.isEmpty()) {
            int u = queue.poll();
            for (int v : e[u])
                if (!visited[v]) {
                    visited[v] = true;
                    dist[v] = dist[u] + 1;
                    queue.add(v);
                    pre[v] = u;
                }
        }
    }

    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        if (n <= 0) return new ArrayList<>();
        this.n = n;
        e = new List[n];
        for (int i = 0; i < n; i++)
            e[i] = new ArrayList<>();
        for (int[] pair : edges) {
            int u = pair[0];
            int v = pair[1];
            e[u].add(v);
            e[v].add(u);
        }

        int[] d1 = new int[n];
        int[] d2 = new int[n];
        int[] pre = new int[n];
        bfs(0, d1, pre);
        int u = 0;
        for (int i = 0; i < n; i++)
            if (d1[i] > d1[u]) u = i;

        bfs(u, d2, pre);
        int v = 0;
        for (int i = 0; i < n; i++)
            if (d2[i] > d2[v]) v = i;

        List<Integer> list = new ArrayList<>();
        while (v != -1) {
            list.add(v);
            v = pre[v];
        }

        if (list.size() % 2 == 1) return Arrays.asList(list.get(list.size() / 2));
        else return Arrays.asList(list.get(list.size() / 2 - 1), list.get(list.size() / 2));
    }
}
```

####模拟topological
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
