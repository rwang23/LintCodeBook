##Peeking Iterator
	Total Accepted: 18259 Total Submissions: 54664 Difficulty: Medium
	Given an Iterator class interface with methods: next() and hasNext(), design and implement a PeekingIterator that support the peek() operation -- it essentially peek() at the element that will be returned by the next call to next().

	Here is an example. Assume that the iterator is initialized to the beginning of the list: [1, 2, 3].

	Call next() gets you 1, the first element in the list.

	Now you call peek() and it returns 2, the next element. Calling next() after that still return 2.

	You call next() the final time and it returns 3, the last element. Calling hasNext() after that should return false.

####思路
- cache下一个元素就可以了

```java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    Iterator<Integer> iterator;
    boolean isPeek;
    Integer cache;
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    this.iterator = iterator;
	    isPeek = false;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
	    if (!isPeek) {
            isPeek = true;
            cache = iterator.next();
	    }
        return cache;
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if (!isPeek) {
	        return iterator.next();
	    } else {
	        isPeek = false;
	        return cache;
	    }
	}

	@Override
	public boolean hasNext() {
	    return isPeek ? true : iterator.hasNext();
	}
}
```
