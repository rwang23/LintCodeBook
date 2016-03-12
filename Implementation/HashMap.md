###HashMap


```java
public class MyHashMap<K, V> {
	private class MapEntry {
		K key;
		V value;
		MapEntry next;
		MapEntry(K key, V value) {
			this.key = key;
			this.value = value;
		}
	}

	private int size = 0;
	private int capacity;
	MapEntry[] entry;

	@SuppressWarnings("unchecked")
	MyHashMap() {
		capacity = 10;
		entry =  (MapEntry[]) new Object[capacity];
	}

	@SuppressWarnings("unchecked")
	MyHashMap(int capacity) {
		entry =  (MapEntry[]) new Object[capacity];
	}

	public void put(K key, V value) {
		int hash = hashCode(key);
		MapEntry newNode = new MapEntry(key, value);
		if (entry[hash % capacity] == null) {
			entry[hash % capacity] = newNode;
		} else {
			if (key == entry[hash % capacity].key) {
				entry[hash % capacity].value = value;
			} else {
				MapEntry nextNode = entry[hash % capacity].next;
				while (nextNode != null) {
					if (key == nextNode.key) {
						nextNode.value = value;
						return;
					}
					nextNode = nextNode.next;
				}
				nextNode = newNode;
			}
		}
	}

	public V get(K key) {
		int hash = hashCode(key);
		MapEntry node = entry[hash % capacity];
		if (node == null) {
			return null;
		}

		if (node.key == key) {
			return node.value;
		}

		while (key != node.key) {
			node = node.next;
			if (node.key == key) {
				return node.value;
			}
		}
		return null;
	}

	public boolean contains(K key) {
		return get(key) != null;
	}

	public int size() {
		return size;
	}

	public void remove(K key) {
		int hash = hashCode(key);
		MapEntry node = entry[hash % capacity];
		if (node == null) return;
		if (key == node.key) {
			entry[hash % capacity] = node.next;
		}

		MapEntry pre = node;
		while (key != node.key) {
			node = node.next;
			if (key == node.key) {
				pre.next = node.next;
				return;
			}
			pre = pre.next;
		}
	}

	private int hashCode(K key) {
		return Math.abs(key.hashCode());
	}

	public void display(){
       for(int i = 0; i < capacity; i++){
           if(entry[i] != null){
            	MapEntry node = entry[i];
                while(node != null){
                    System.out.print("{" + node.key + "=" + node.value + "}" + " ");
                    node = node.next;
                }
           }
       }
    }

    public static void main(String[] args) {
    	MyHashMap<Integer, Integer> hashMapCustom = new MyHashMap<Integer, Integer>();
        hashMapCustom.put(21, 12);
        hashMapCustom.put(25, 121);
        hashMapCustom.put(30, 151);
        hashMapCustom.put(33, 15);
        hashMapCustom.put(35, 89);

        System.out.println("value corresponding to key 21="
                     + hashMapCustom.get(21));
        System.out.println("value corresponding to key 51="
                     + hashMapCustom.get(51));

        System.out.print("Displaying : ");
        hashMapCustom.display();
        //System.out.println("\n\nvalue corresponding to key 21 removed: " + hashMapCustom.remove(21));
        //System.out.println("value corresponding to key 51 removed: "+ hashMapCustom.remove(51));

        System.out.print("Displaying : ");
        hashMapCustom.display();
    }
}
```


