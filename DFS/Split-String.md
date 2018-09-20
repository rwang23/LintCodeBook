##Split String
  Give a string, you can choose to split the string after one character or two adjacent characters, 
  and make the string to be composed of only one character or two characters. Output all possible results.

##Example
  Given the string "123"
  return [["1","2","3"],["12","3"],["1","23"]]
  
##思路
- 注意点，只有从1开始的，而不是遍历一边1,2,3
- 加入结果的时候，要是一个新的list，不然用本来的，一直在dfs中被改变



```java
public class Solution {
    /*
     * @param : a string to be split
     * @return: all possible split string array
     */
    public List<List<String>> splitString(String s) {
        // write your code here
        List<List<String>> results = new ArrayList<List<String>>();
        List<String> splitResult = new ArrayList<String>();
        if (s == null || s.equals("")) {
            results.add(splitResult);
            return results;
        }
        dfs(results, splitResult, s, 0);
        
        return results;
    }
    
    public void dfs(List<List<String>> results, List<String> splitResult, String s, int index) {
        
        if (index >= s.length()) {
            List<String> result = new ArrayList<String>(splitResult);
            results.add(result);
            return;
        }
        
        for (int len = 1; len < 3; len++) {
            if (index + len > s.length()) {
                continue;
            }
            String cur = s.substring(index, index + len);
            splitResult.add(cur);
            dfs(results, splitResult, s, index + len);
            splitResult.remove(splitResult.size() - 1);
        }
        
        
    }
}
```
