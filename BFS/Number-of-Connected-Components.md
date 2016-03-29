##Number of Connected Components in an Undirected Graph

	Total Accepted: 5832 Total Submissions: 13633 Difficulty: Medium
	Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

	Example 1:
	     0          3
	     |          |
	     1 --- 2    4
	Given n = 5 and edges = [[0, 1], [1, 2], [3, 4]], return 2.

	Example 2:
	     0           4
	     |           |
	     1 --- 2 --- 3
	Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]], return 1.

####思路
- BFS/DFS/Union Find 三种方法

####Union Find
```java
public class Solution {
    public int countComponents(int n, int[][] edges) {
        if (n <= 0) {
            return 0;
        }

        int length = edges.length;
        int[] parent = new int[n];

        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }

        for (int i = 0; i < length; i++) {
            int a = edges[i][0];
            int b = edges[i][1];
            union(parent, a, b);
        }

        Set<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < n; i++) {
            if (set.contains(find(parent, i))) {
                continue;
            } else {
                set.add(find(parent, i));
            }
        }
        return set.size();
    }

    public int find(int[] parent, int x) {
        int father = parent[x];
        while (father != parent[father]) {
            father = parent[father];
        }

        while (x != parent[x]) {
            int temp = parent[x];
            parent[x] = father;
            x = temp;
        }
        return father;
    }

    public void union(int[] parent, int a, int b) {
        int root_a = find(parent, a);
        int root_b = find(parent, b);

        if (root_a != root_b) {
            parent[root_a] = root_b;
        }
    }
}
```

####BFS
```java
public class Solution {

    private class Node {
        private int id;
        private List<Integer> neighbor;
        Node(int id) {
            this.id = id;
            neighbor = new ArrayList<Integer>();
        }
    }
    public int countComponents(int n, int[][] edges) {
        if (n <= 0) {
            return 0;
        }

        Node[] list = new Node[n];
        for (int i = 0; i < n; i++) {
            list[i] = new Node(i);
        }
        for (int i = 0; i < edges.length; i++) {
            int cur = edges[i][0];
            int next = edges[i][1];
            list[cur].neighbor.add(next);
            list[next].neighbor.add(cur);
        }

        int count = 0;
        boolean[] visited = new boolean[n];
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                Queue<Integer> queue = new LinkedList<Integer>();
                queue.offer(i);
                visited[i] = true;
                while (!queue.isEmpty()) {
                    int cur = queue.poll();
                    Node curNode = list[cur];
                    for (Integer next : curNode.neighbor) {
                        if (!visited[next]) {
                            queue.offer(next);
                            visited[next] = true;
                        }
                    }
                }
                count++;
            }
        }
        return count;
    }
}
```

####DFS
