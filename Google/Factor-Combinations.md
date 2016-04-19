##Factor Combinations
    Total Accepted: 7418 Total Submissions: 21527 Difficulty: Medium
    Numbers can be regarded as product of its factors. For example,

    8 = 2 x 2 x 2;
      = 2 x 4.
    Write a function that takes an integer n and return all possible combinations of its factors.

    Note:
    Each combination's factors must be sorted ascending, for example: The factors of 2 and 6 is [2, 6], not [6, 2].
    You may assume that n is always positive.
    Factors should be greater than 1 and less than n.
    Examples:
    input: 1
    output:
    []
    input: 37
    output:
    []
    input: 12
    output:
    [
      [2, 6],
      [2, 2, 3],
      [3, 4]
    ]
    input: 32
    output:
    [
      [2, 16],
      [2, 2, 8],
      [2, 2, 2, 4],
      [2, 2, 2, 2, 2],
      [2, 4, 4],
      [4, 8]
    ]

####思路
- DFS,不断找,然后如果已经包含了相同的List,就不加入
- 因为判断重复,所以多进入了很多步骤,导致时间比较高,可以优化

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (n <= 3) {
            return result;
        }
        List<Integer> list = new ArrayList<Integer>();
        dfs(result, list, n);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> list, int n) {
        if (n == 1) {
            if (list.size() == 1) {
                return;
            }
            List<Integer> newList = new ArrayList<Integer>(list);
            Collections.sort(newList);
            if (!result.contains(newList)) {
                result.add(newList);
            }
            return;
        }

        for (int i = 2; i <= n; i++) {
            if (n % i == 0) {
                list.add(i);
                dfs(result, list, n / i);
                list.remove(list.size() - 1);
            }
        }
    }
}
```

####优化1
- 加入start参数,使得 i = start,然后传入i,
- 如果这样不会重复找以前已经有的

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (n <= 3) {
            return result;
        }
        List<Integer> list = new ArrayList<Integer>();
        dfs(result, list, n, 2);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> list, int n, int start) {
        if (n == 1) {
            if (list.size() == 1) {
                return;
            }
            List<Integer> newList = new ArrayList<Integer>(list);
            Collections.sort(newList);
            if (!result.contains(newList)) {
                result.add(newList);
            }
            return;
        }

        for (int i = start; i <= n; i++) {
            if (n % i == 0) {
                list.add(i);
                dfs(result, list, n / i, i);
                list.remove(list.size() - 1);
            }
        }
    }
}
```

####优化2
- 每次加进两个数,
- 然后再去除掉一个,然后对这个数进行递归
- 这样限制也变成了Math.sqrt(n)

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> ret = new LinkedList<List<Integer>>();
        if(n <= 3)  return ret;
        List<Integer> path = new LinkedList<Integer>();
        getFactors(2, n, path, ret);
        return ret;
    }

    private void getFactors(int start, int n, List<Integer> path, List<List<Integer>> ret){
       for(int i = start; i <= Math.sqrt(n); i++){
           if(n % i == 0 && n/i >= i){  // The previous factor is no bigger than the next
               path.add(i);
               path.add(n/i);
               ret.add(new LinkedList<Integer>(path));
               path.remove(path.size() - 1);
               getFactors(i, n/i, path, ret);
               path.remove(path.size() - 1);
           }
       }
    }
}
```
