##Course Schedule

	Total Accepted: 36632 Total Submissions: 137196 Difficulty: Medium
	There are a total of n courses you have to take, labeled from 0 to n - 1.

	Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

	Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

	For example:

	2, [[1,0]]
	There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

	2, [[1,0],[0,1]]
	There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

####思路
- topological order

```java
/*
topological sort

step1:
calculate the indegree of every course
step2:
push the course with 0 indegree int o the queue
step3:
bfs traverse queue,
decrease the indegree after one course is traversed and push new 0 indegree course into the queue

if all course is traversed, then return true
otherwise return false
*/

public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        if (prerequisites == null || prerequisites.length == 0 || prerequisites[0].length == 0) {
            return true;
        }

        int[] indegrees = new int[numCourses];
        int size = prerequisites.length;
        Map<Integer, List<Integer>> map = new HashMap<Integer, List<Integer>>();
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
                }
            }
        }

        for (int i = 0; i < numCourses; i++) {
            if (indegrees[i] != 0) {
                return false;
            }
        }
        return true;
    }
}
```
