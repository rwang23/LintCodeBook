###Trie
[princeton](http://algs4.cs.princeton.edu/52trie/TrieST.java.html)

```java
public class Trie<Value> {

	private class Node {
		private Node[] next = (Node []) new Object[R];
		private Value value;
	}

	private static final int R =256;
	private Node root = new Node();
	private int size = 0;

	public void put(String s, Value value) {
		put(root, s, 0, value);
	}

	public Node put(Node root, String s, int index, Value value) {
		if (root == null) {
			root = new Node();
		}

		if (s.length() == index) {
			root.value = value;
			size++;
			return root;
		}

		char c = s.charAt(index);
		root.next[c] = put(root.next[c], s, index + 1, value);

		return root;

	}

	public Value get(String s) {
		return get(root, s, 0);
	}

	public Value get(Node root, String s, int index) {
		if (root == null) {
			return null;
		}

		if (s.length() == index) {
			return root.value;
		}

		char c = s.charAt(index);
		return get(root.next[c], s, index + 1);

	}

	public boolean contains(String s) {
		return get(s) != null;
	}

   public Iterable<String> keys() {
        return keysWithPrefix("");
    }

    /**
     * Returns all of the keys in the set that start with <tt>prefix</tt>.
     * @param prefix the prefix
     * @return all of the keys in the set that start with <tt>prefix</tt>,
     *     as an iterable
     */
    public Iterable<String> keysWithPrefix(String prefix) {
        Queue<String> results = new Queue<String>();
        Node x = get(root, prefix, 0);
        collect(x, new StringBuilder(prefix), results);
        return results;
    }

    private void collect(Node x, StringBuilder prefix, Queue<String> results) {
        if (x == null) return;
        if (x.val != null) results.enqueue(prefix.toString());
        for (char c = 0; c < R; c++) {
            prefix.append(c);
            collect(x.next[c], prefix, results);
            prefix.deleteCharAt(prefix.length() - 1);
        }
    }


}
```
