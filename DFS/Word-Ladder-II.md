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
- 直接DFS，但是会超memory

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
