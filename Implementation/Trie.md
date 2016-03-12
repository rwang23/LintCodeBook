###Trie

```java
public class Trie<Value> {

	private class Node {
		private Node[] next = (Node []) new Object[R];
		private Value value;
	}

	private static final int R =256;
	private Node root = new Node();

	public void put(String s, Value value) {
		put(root, s, 0, value);
	}

	public Node put(Node root, String s, int index, Value value) {
		if (root == null) {
			root = new Node();
		}

		if (s.length() == index) {
			root.value = value;
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
}
```
