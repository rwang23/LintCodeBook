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

####后来写的,在hasNext()里边进行操作
- 注意i.next()的类型转化
- 或者在声明的时候
- Iterator<List<Integer>> it;
- Iterator<Integer> curr;
- 而不是简单Iterator
- 每当i2是null的时候,就是还没赋值,或者说,i1有,但是i2已经为空,就需要进入下一轮迭代,
- 但是有可能出现[]这样的空集,这会i2还是为空,所以要用while

```java
public class Vector2D implements Iterator<Integer> {

    private Iterator i1;
    private Iterator i2;
    public Vector2D(List<List<Integer>> vec2d) {
        i1 = vec2d.iterator();
    }

    @Override
    public Integer next() {
        return (Integer)i2.next();
    }

    @Override
    public boolean hasNext() {
        while ((i2 == null || !i2.hasNext()) && i1.hasNext()) {
            List<Integer> list = (List<Integer>)i1.next();
            i2 = list.iterator();
        }

        // while (i2 != null && !i2.hasNext() && i1.hasNext()) {
        //     List<Integer> list = (List<Integer>)i1.next();
        //     i2 = list.iterator();
        // }
        if (i2 == null) {
           return false;
        }

        return i1.hasNext() || i2.hasNext();
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
