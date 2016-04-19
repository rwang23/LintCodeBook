##Course Schedule II

	Total Accepted: 24916 Total Submissions: 118970 Difficulty: Medium
	There are a total of n courses you have to take, labeled from 0 to n - 1.

	Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

	Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

	There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

	For example:

	2, [[1,0]]
	There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1]

	4, [[1,0],[2,0],[3,1],[3,2]]
	There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. So one correct course order is [0,1,2,3]. Another correct ordering is[0,2,1,3].

	Note:
	The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.

####思路
- 跟I一模一样,就是输出换了
- 同时注意一下,如果 prerequisites.length == 0 并不是输出new int[0],可能只是没有限制条件,但是一样有课程呀

```java
public class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        if (prerequisites == null) {
            return new int[0];
        }

        int[] indegrees = new int[numCourses];
        int size = prerequisites.length;
        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
        int node = 0;
        int[] result = new int[numCourses];

        for (int i = 0; i < size; i++) {
            int pre = prerequisites[i][1];
            int cur = prerequisites[i][0];
            indegrees[cur]++;
            if (!map.containsKey(pre)) {
                List<Integer> neighbor = new ArrayList<Integer>();
                neighbor.add(cur);
                map.put(pre, neighbor);
            } else {
                map.get(pre).add(cur);
            }
        }

        Queue<Integer> queue = new LinkedList<Integer>();
        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] == 0) {
                queue.offer(i);
                result[node++] = i;
            }
        }

        while (!queue.isEmpty()) {
            int pre = queue.poll();
            if (!map.containsKey(pre)) {
                continue;
            }
            List<Integer> neighbor = map.get(pre);
            for (int i = 0; i < neighbor.size(); i++) {
                int cur = neighbor.get(i);
                indegrees[cur]--;
                if (indegrees[cur] == 0) {
                    queue.offer(cur);
                    result[node++] = cur;
                }
            }
        }

        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] != 0) {
                return new int[0];
            }
        }
        return result;
    }
}
```
