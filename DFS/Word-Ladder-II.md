##Word Ladder II

  Given two words (start and end), and a dictionary, find all shortest transformation sequence(s) from start to end, such that:

  Only one letter can be changed at a time
  Each intermediate word must exist in the dictionary


##Example

  Given:
  start = "hit"
  end = "cog"
  dict = ["hot","dot","dog","lot","log"]

  Return

  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]
  Notice
  All words have the same length.
  All words contain only lowercase alphabetic characters.
  
  
##解法
- 直接DFS，但是会超memory,应该思考优化和剪枝
- 使用BFS把start到end最短路徑level中的graph建立起來
- 使用DFS找出所有的ladders

###直接DFS
```java
public class Solution {
    /*
     * @param start: a string
     * @param end: a string
     * @param dict: a set of string
     * @return: a list of lists of string
     */
     
    int minSteps = Integer.MAX_VALUE;
    List<List<String>> results = new ArrayList<List<String>>();
    public List<List<String>> findLadders(String start, String end, Set<String> dict) {
        // write your code here
        
        Map<String, Boolean> visited = new HashMap<String, Boolean>();
        List<String> list = new ArrayList<String>();
        list.add(start);
        populateMap(visited, dict);
        visited.put(end, false);
        dfs(visited, list, start, end, 0);
        return results;
    }
    
    public void dfs(Map<String, Boolean> visited, List<String> list, String start, String target, int steps) {
        
        if (steps > minSteps) {
            return;
        }
        
        if (start.equals(target)) {
            if (steps < minSteps) {
                minSteps = steps;
                results = new ArrayList<List<String>>();
                results.add(new ArrayList<String>(list));
            } else if (steps == minSteps) {
                results.add(new ArrayList<String>(list));
            } 
            return;
        }
        
        for (int i = 0; i < start.length(); i++) {
            for (char ch = 'a'; ch <= 'z'; ch++) {
                StringBuilder sb = new StringBuilder("");
                sb.append(start.substring(0, i));
                sb.append(ch);
                sb.append(start.substring(i + 1, start.length()));
                String transform = sb.toString();
                
                if (!visited.containsKey(transform)) {
                    continue;
                } else {
                    if (visited.get(transform)) {
                        continue;
                    }
                }

                visited.put(transform, true);
                list.add(transform);
                steps++;
                dfs(visited, list, transform, target, steps);
                steps--;
                list.remove(list.size() - 1);
                visited.put(transform, false);
            }
        }
    }
    
    
    public void populateMap( Map<String, Boolean> map, Set<String> set) {
        for (String s : set) {
            map.put(s, false);
        }
    }
}
```

##九章解法
- start -> end: bfs， 先BFS建立最短距离map，算好每个点到起始点的距离，同时建立一个map，知道点A能够到点B，方便DFS
- end -> start: dfs， 因为上面有个点A到点B的map，所以DFS需要反过来，end->start

```
public class Solution {
    public List<List<String>> findLadders(String start, String end,
            Set<String> dict) {
        List<List<String>> ladders = new ArrayList<List<String>>();
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        Map<String, Integer> distance = new HashMap<String, Integer>();

        dict.add(start);
        dict.add(end);
 
        bfs(map, distance, start, end, dict);
        
        List<String> path = new ArrayList<String>();
        
        dfs(ladders, path, end, start, distance, map);

        return ladders;
    }

    void dfs(List<List<String>> ladders, List<String> path, String crt,
            String start, Map<String, Integer> distance,
            Map<String, List<String>> map) {
        path.add(crt);
        if (crt.equals(start)) {
            Collections.reverse(path);
            ladders.add(new ArrayList<String>(path));
            Collections.reverse(path);
        } else {
            for (String next : map.get(crt)) {
                if (distance.containsKey(next) && distance.get(crt) == distance.get(next) + 1) { 
                    dfs(ladders, path, next, start, distance, map);
                }
            }           
        }
        path.remove(path.size() - 1);
    }

    void bfs(Map<String, List<String>> map, Map<String, Integer> distance,
            String start, String end, Set<String> dict) {
        Queue<String> q = new LinkedList<String>();
        q.offer(start);
        distance.put(start, 0);
        for (String s : dict) {
            map.put(s, new ArrayList<String>());
        }
        
        while (!q.isEmpty()) {
            String crt = q.poll();

            List<String> nextList = expand(crt, dict);
            for (String next : nextList) {
                map.get(next).add(crt);
                if (!distance.containsKey(next)) {
                    distance.put(next, distance.get(crt) + 1);
                    q.offer(next);
                }
            }
        }
    }

    List<String> expand(String crt, Set<String> dict) {
        List<String> expansion = new ArrayList<String>();

        for (int i = 0; i < crt.length(); i++) {
            for (char ch = 'a'; ch <= 'z'; ch++) {
                if (ch != crt.charAt(i)) {
                    String expanded = crt.substring(0, i) + ch
                            + crt.substring(i + 1);
                    if (dict.contains(expanded)) {
                        expansion.add(expanded);
                    }
                }
            }
        }

        return expansion;
    }
}
```
