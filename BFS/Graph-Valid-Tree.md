##Graph Valid Tree
	Total Accepted: 10169 Total Submissions: 31882 Difficulty: Medium
	Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

	For example:

	Given n = 5 and edges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.

	Given n = 5 and edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

####思路
- 首先想到了BFS的方法
- 1.暴力做法去得到每个点的neighbor, O(n2)
- 2.然后想到了用hashmap, Map<Integer, List<Integer>> 这样O(n)就能得到neighbor点
- 得到了neighbor点,就只需要BFS就可以了,注意不是valid的条件,就是两个点(不包括之前遍历的)指向了同一个点,或者有的点没有neighbor,这样就不能构成tree
- 最终时间复杂度还是O(n),但是跑出来的速度还是很慢

```java
public class Solution {
    /**
     * @param n an integer
     * @param edges a list of undirected edges
     * @return true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // Write your code here
        if (n <= 0) {
            return false;
        }

        if (n == 1) {
            return true;
        }

        if (edges.length * 2 < n) {
            return false;
        }

        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
        int[] occur = new int[n];

        for (int i = 0; i < edges.length; i++) {

            int cur = edges[i][0];
            int direction = edges[i][1];
            occur[cur]++;
            occur[direction]++;

            if (!map.containsKey(cur)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(direction);
                map.put(cur, list);
            } else {
                List<Integer> list = map.get(cur);
                list.add(direction);
                map.put(cur, list);
            }

            if (!map.containsKey(direction)) {
                List<Integer> list = new ArrayList<Integer>();
                list.add(cur);
                map.put(direction, list);
            } else {
                List<Integer> list = map.get(direction);
                list.add(cur);
                map.put(direction, list);
            }
        }

        for (int i = 0; i < n; i++) {
            if (occur[i] == 0) {
                return false;
            }
        }

        int[] visited = new int[n];
        Queue<Integer> queue = new LinkedList<Integer>();
        queue.offer(0);
        visited[0] = 1;

        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int cur = queue.poll();
                List<Integer> neighbor = map.get(cur);
                if (neighbor == null) {
                    continue;
                }

                for (int j = 0; j < neighbor.size(); j++) {
                    int next = neighbor.get(j);
                    if (!map.containsKey(next)) {
                        continue;
                    }
                    if (visited[next] == 1) {
                        return false;
                    }
                    queue.offer(next);
                    visited[next] = 1;
                }
                map.remove(cur);
            }
        }

        return map.size() == 0 ? true : false;
    }
}
```
