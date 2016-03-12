###UnionFind

```java
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
			parent = map.get(father);
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
		int root_x = find(u1);
		int root_y = find(u2);
		if (root_x != root_y) {
			map.put(root_x, root_y);
		}
	}

	public boolean connected(int p, int q) {
		return find(p) == find(q);
	}

}
```
