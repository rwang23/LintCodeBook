##Flatten Nested List Iterator

	Total Accepted: 723 Total Submissions: 3985 Difficulty: Medium
	Given a nested list of integers, implement an iterator to flatten it.

	Each element is either an integer, or a list -- whose elements may also be integers or other lists.

	Example 1:
	Given the list [[1,1],2,[1,1]],

	By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,1,2,1,1].

	Example 2:
	Given the list [1,[4,[6]]],

	By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,4,6].

####思路
- 这道题看上去似曾相似,果然好像做过一道题叫做 Nested List Weight Sum
- 所以我这道题一来也直接做了递归
- 没想出来更好的办法,想了一个while把自己绕进去了,应该用stack是可以做的

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

public class NestedIterator implements Iterator<Integer> {

    private List<Integer> list = new ArrayList<Integer>();
    private int size;
    private int iterate = 0;
    public NestedIterator(List<NestedInteger> nestedList) {
        dfs(nestedList);
        size = list.size();
    }

    public void dfs(List<NestedInteger> nestedList) {
        if (nestedList == null) {
            return;
        }
        int size = nestedList.size();
        for (int i = 0; i < size; i++) {
            NestedInteger cur = nestedList.get(i);
            if (cur.isInteger()) {
                list.add(cur.getInteger());
            } else {
                dfs(cur.getList());
            }
        }
    }

    @Override
    public Integer next() {
        return list.get(iterate++);
    }

    @Override
    public boolean hasNext() {
        return iterate < size;
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
