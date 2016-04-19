###Queue Implementation
```java
import java.util.Iterator;

public class MyQueue<Item> implements Iterable<Item> {
	private class Node {
		Item val;
		Node next;
		Node(Item val) {
			this.val = val;
		}
	}

	private Node head = null;
	private Node tail = null;
	private int size;

	MyQueue() {
		this.size = 0;
	}

	public void offer(Item item) {
		Node node = new Node(item);
		if (head == null) {
		head = node;
		tail = node;
		} else {
			Node oldtail = tail;
			oldtail.next = node;
			tail = node;
		}
		size++;
	}

	public Item poll() {

		if (head == null) {
			return null;
		}
		Item oldItem = head.val;
		head = head.next;
		if (head == null) {
			tail = null;
		}
		size--;
		return oldItem;
	}

	public boolean isEmpty() {
		return head == null;
	}

	public int size() {
		return size;
	}

	public Iterator<Item> iterator() {
		return new queueIterator();
	}

	private class queueIterator implements Iterator<Item> {

		private int i = size;
		private Node oldhead = head;
		public boolean hasNext() {
			return i != 0;
		}
		public Item next() {
			Item cur = oldhead.val;
			oldhead = oldhead.next;
			i--;
			return cur;
		}

		public void remove() {
			throw new UnsupportedOperationException();
		}
	}

	public static void main(String[] args) {
		MyQueue<String> q = new MyQueue<String>();
		q.offer("first");
		q.offer("second");
		q.offer("third");
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("First test");
		q.poll();
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("Second test");
		q.offer("fourth");
		q.offer("fifth");
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("Third test");
	}


}
```
