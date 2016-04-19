##Number of Islands II

	Total Accepted: 4722 Total Submissions: 14060 Difficulty: Hard
	A 2d grid map of m rows and n columns is initially filled with water.
	We may perform an addLand operation which turns the water at position (row, col) into a land.
	Given a list of positions to operate, count the number of islands after each addLand operation.
	An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.
	You may assume all four edges of the grid are all surrounded by water.

	Example:

	Given m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]].
	Initially, the 2d grid grid is filled with water. (Assume 0 represents water and 1 represents land).

	0 0 0
	0 0 0
	0 0 0
	Operation #1: addLand(0, 0) turns the water at grid[0][0] into a land.

	1 0 0
	0 0 0   Number of islands = 1
	0 0 0
	Operation #2: addLand(0, 1) turns the water at grid[0][1] into a land.

	1 1 0
	0 0 0   Number of islands = 1
	0 0 0
	Operation #3: addLand(1, 2) turns the water at grid[1][2] into a land.

	1 1 0
	0 0 1   Number of islands = 2
	0 0 0
	Operation #4: addLand(2, 1) turns the water at grid[2][1] into a land.

	1 1 0
	0 0 1   Number of islands = 3
	0 1 0
	We return the result as an array: [1, 1, 2, 3]

	Challenge:

	Can you do it in time complexity O(k log mn), where k is the length of the positions?

####思路
- 直接暴力BFS O(kmn)
- UnionFind O(klogmn)
- 明白用Union Find问题就简单多了


```java
public class Solution {
    public List<Integer> numIslands2(int m, int n, int[][] positions) {
        List<Integer> result = new ArrayList<Integer>();
        if (positions.length == 0 || positions[0].length == 0) {
            return result;
        }

        int[] parent = new int[m * n + 1];
        int count = 0;
        int[] xstep = new int[]{0,  0, 1, -1};
        int[] ystep = new int[]{1, -1, 0,  0};

        int k = positions.length;
        for (int x = 0; x < k; x++) {
            int i = positions[x][0];
            int j = positions[x][1];
            int index = i * n + j + 1;
            parent[index] = index;
            count++;
            for (int d = 0; d < 4; d++) {
                int newX = i + xstep[d];
                int newY = j + ystep[d];
                if (newX < m && newY < n && newX >= 0 && newY >= 0) {
                    int newIndex = newX * n + newY + 1;
                    if (find(newIndex, parent) == find(index, parent)) {
                        continue;
                    }
                    if (parent[newIndex] != 0) {
                        union(index, newIndex, parent);
                        count--;
                    }
                }
            }
            result.add(count);
        }
        return result;
    }

    public int find(int x, int[] parent) {
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

    public void union(int x, int y, int[] parent) {
        int root_x = find(x, parent);
        int root_y = find(y, parent);
        if (root_x != root_y) {
            parent[root_y] = root_x;
        }
    }
}
```

