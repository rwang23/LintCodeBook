##Nested List Weight Sum

	Total Accepted: 514 Total Submissions: 902 Difficulty: Easy
	Given a nested list of integers, return the sum of all integers in the list weighted by their depth.

	Each element is either an integer, or a list -- whose elements may also be integers or other lists.

	Example 1:
	Given the list [[1,1],2,[1,1]], return 10. (four 1's at depth 2, one 2 at depth 1)

	Example 2:
	Given the list [1,[4,[6]]], return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27)

####思路
- 最开始想用while,但是发现函数是复用的,所以不如直接递归

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {

    public int depthSum(List<NestedInteger> nestedList) {
        if (nestedList == null) {
            return 0;
        }
        return depthSum(nestedList, 1);
    }
    public int depthSum(List<NestedInteger> nestedList, int depth) {
        if (nestedList == null) {
            return 0;
        }

        int sum = 0;
        int len = nestedList.size();
        for (int i = 0; i < len; i++) {
            NestedInteger cur = nestedList.get(i);
            int j = 0;
            if (cur.isInteger()) {
                sum += cur.getInteger() * depth;
            } else {
                sum += depthSum(cur.getList(), depth + 1);
            }
        }
        return sum;
    }
}
```
