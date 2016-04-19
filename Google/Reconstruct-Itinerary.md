##Reconstruct Itinerary

	Total Accepted: 7807 Total Submissions: 33158 Difficulty: Medium

	Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order.
	All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

	Note:
	If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.
	For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
	All airports are represented by three capital letters (IATA code).
	You may assume all tickets form at least one valid itinerary.
	Example 1:
	tickets = [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
	Return ["JFK", "MUC", "LHR", "SFO", "SJC"].
	Example 2:
	tickets = [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
	Return ["JFK","ATL","JFK","SFO","ATL","SFO"].
	Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.

####思路
- [参考](http://www.cnblogs.com/EdwardLiu/p/5184961.html)

```java
public class Solution {
    LinkedList<String> res;
    Map<String, PriorityQueue<String>> mp;

    public List<String> findItinerary(String[][] tickets) {
        if (tickets==null || tickets.length==0) return new LinkedList<String>();
        res = new LinkedList<String>();
        mp = new HashMap<String, PriorityQueue<String>>();
        for (String[] ticket : tickets) {
            if (!mp.containsKey(ticket[0])) {
                mp.put(ticket[0], new PriorityQueue<String>());
            }
            mp.get(ticket[0]).offer(ticket[1]);
        }
        dfs("JFK");
        return res;
    }

    public void dfs(String cur) {
        while (mp.containsKey(cur) && !mp.get(cur).isEmpty()) {
            dfs(mp.get(cur).poll());
        }
        res.addFirst(cur);
    }
}
```
