###Deque

```java
import java.util.Iterator;

public class MyDeque<Item> implements Iterable<Item>{
	private class Node {
		Node next;
		Node pre;
		Item item;
		Node(Item item) {
			this.item = item;
		}
	}

	private int size = 0;
	private Node head;
	private Node tail;

	public void offerFirst(Item item) {
		Node newNode = new Node(item);
		if (head == null) {
			head = newNode;
			tail = newNode;
		} else {
			newNode.next = head;
			head.pre = newNode;
			head = newNode;
		}
		size++;
	}

	public void offerLast(Item item) {
		Node newNode = new Node(item);
		if (tail == null) {
			head = newNode;
			tail = newNode;
		} else {
			tail.next = newNode;
			newNode.pre = tail;
			tail = newNode;
		}
		size++;

	}

	public Item pollFirst(Item item) {
		Node temp = head;
		if (head == null) {
			throw new NullPointerException();
		} else {
			head = head.next;
			head.pre = null;
		}
		size--;
		return temp.item;
	}

	public Item pollLast(Item item) {
		Node temp = head;
		if (tail == null) {
			throw new NullPointerException();
		} else {
			Node last = tail.pre;
			last.next = null;
			last = tail;
		}
		size--;
		return temp.item;
	}

	public boolean isEmpty() {
		return size == 0;
	}

	public int size() {
		return size;
	}

	public Iterator<Item> iterator() {
		return new MyDequeIterator();
	}

	private class MyDequeIterator implements Iterator<Item> {

		Node cur = head;
		int i = size;
		public boolean hasNext() {
			return i != 0;
		}

		public Item next() {
			Node temp = cur;
			cur = cur.next;
			return temp.item;
		}
	}

}

```
