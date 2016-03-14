###Stack
```java
import java.util.Iterator;

public class MyStack<Item> implements Iterable<Item> {

	private class Node{
		Item item;
		Node next;
		Node(Item item) {
			this.item = item;
		}
	}

	private Node head = null;
	private int size = 0;

	public Item pop() {
		Node old = head;
		if (size == 0) {
			throw new NullPointerException();
		} else {
			head = head.next;
			size--;
		}
		return old.item;
	}

	public void push(Item item) {
		Node newNode = new Node(item);
		if (head == null) {
			head = newNode;
		} else {
			newNode.next = head;
			head = newNode;
		}
		size++;
	}

	public int size() {
		return size;
	}

	public boolean isEmpty() {
		return size == 0;
	}

	public Iterator<Item> iterator() {
		return new MyStackIterator();
	}

	private class MyStackIterator implements Iterator<Item> {

		private int i = size;
		private Node  cur = head;
		public boolean hasNext() {
			return i != 0;
		}

		public Item next() {
			Node old = cur;
			cur = cur.next;
			i--;
			return old.item;
		}

		public void remove () {
			throw new UnsupportedOperationException();
		}
	}

	public static void main(String[] args) {
		MyStack<String> q = new MyStack<String>();
		System.out.println("Mystack test");
		q.push("first");
		q.push("second");
		q.push("third");
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("First test");
		q.pop();
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("Second test");
		q.push("fourth");
		q.push("fifth");
		q.pop();
		for (String s : q) {
			System.out.println(s);
		}
		System.out.println("Third test");
	}

}


```
