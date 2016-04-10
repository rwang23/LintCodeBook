##Flatten 2D Vector

	Total Accepted: 8352 Total Submissions: 24915 Difficulty: Medium
	Implement an iterator to flatten a 2d vector.

	For example,
	Given 2d vector =

	[
	  [1,2],
	  [3],
	  [4,5,6]
	]
	By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].

####思路
- 注意考虑到可能会出现空行的情况

```java
public class Vector2D {

    Iterator<List<Integer>> it;
    Iterator<Integer> curr;

    public Vector2D(List<List<Integer>> vec2d) {
        it = vec2d.iterator();
    }

    public int next() {
        hasNext();
        return curr.next();
    }

    public boolean hasNext() {
        // 当前列表的迭代器为空，或者当前迭代器中没有下一个值时，需要更新为下一个迭代器
        while((curr == null || !curr.hasNext()) && it.hasNext()){
            curr = it.next().iterator();
        }
        return curr != null && curr.hasNext();
    }
}
```
