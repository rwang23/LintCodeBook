###UnionFind

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;


public class UnionFind {

	Map<Integer, Integer> map = new HashMap<Integer, Integer>();

	UnionFind(HashSet<Integer> set) {
		for (Integer i : set) {
			map.put(i, i);
		}
	}

	UnionFind(int[] array) {
		for (int i = 0; i < array.length; i++) {
			map.put(array[i], array[i]);
		}

	}

	UnionFind(ArrayList<Integer> array) {
		for (Integer i : array) {
			map.put(i, i);
		}
	}

	public int find(int x) {
		int parent = map.get(x);
		while (parent != map.get(parent)) {
			parent = map.get(parent);
		}

		int father = map.get(x);
		while (father != map.get(father)) {
			int temp = map.get(father);
			map.put(father, parent);
			father = temp;
		}

		return parent;

	}

	public void union(int x, int y) {
		int root_x = find(x);
		int root_y = find(y);
		if (root_x != root_y) {
			map.put(root_x, root_y);
		}
	}

	public boolean connected(int p, int q) {
		return find(p) == find(q);
	}

}
```

###Generic

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;



public class UnionFind<Item> {

	Map<Item, Item> map = new HashMap<Item, Item>();

	UnionFind(HashSet<Item> set) {
		for (Item i : set) {
			map.put(i, i);
		}
	}

	UnionFind(Item[] array) {
		for (int i = 0; i < array.length; i++) {
			map.put(array[i], array[i]);
		}

	}

	UnionFind(ArrayList<Item> array) {
		for (Item i : array) {
			map.put(i, i);
		}
	}

	public Item find(Item x) {
		Item parent = map.get(x);
		while (parent != map.get(parent)) {
			parent = map.get(parent);
		}

		Item father = map.get(x);
		while (father != map.get(father)) {
			Item temp = map.get(father);
			map.put(father, parent);
			father = temp;
		}

		return parent;

	}

	public void union(Item x, Item y) {
		Item root_x = find(x);
		Item root_y = find(y);
		if (root_x != root_y) {
			map.put(root_x, root_y);
		}
	}

	public boolean connected(Item p, Item q) {
		return find(p) == find(q);
	}

}
```
