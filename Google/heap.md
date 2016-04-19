###MinHeap

```java

public class minheap<Item extends Comparable<Item>> {
	private int size = 0;
	private int capacity;
	private Item[] array;

	@SuppressWarnings("unchecked")
	minheap() {
		this.capacity = 10;
		array = (Item[]) new Comparable[capacity + 1];
	}

	@SuppressWarnings("unchecked")
	minheap(int x) {
		this.capacity = x;
		array = (Item[]) new Comparable[x + 1];
	}

	public void createHeap(Item[] input) {
		if (input.length > 0) {
			for (int i = 0; i < input.length; i++) {
				add(input[i]);
			}
		}
	}

	public void display(){
		for(int i = 1; i < array.length; i++){
			System.out.print(" " + array[i]);
		}
		System.out.println("");
	}

	public void add(Item item) {
		if (size == capacity + 1) {
			if (array[size].compareTo(item) > 0) {
				array[size] = item;
				siftup();
			}
		} else {
			array[++size] = item;
			siftup();
		}
	}

	public void siftup() {
		int i = size;
		while (i > 1 && array[i].compareTo(array[i / 2]) < 0) {
			swap(array, i, i / 2);
			i = i / 2;
		}
	}

	public void swap(Item[] array, int index1, int index2) {
		Item temp = array[index1];
		array[index1] = array[index2];
		array[index2] = temp;
	}

	public void siftdown(int index) {
		int smallest = index;

		while (index <= capacity) {
			if (index * 2  <= size && array[index * 2].compareTo(array[smallest]) < 0) {
				smallest = index * 2;
			}
			if (index * 2 + 1 <= size && array[index * 2 + 1].compareTo(array[smallest]) < 0) {
				smallest = index * 2 + 1;
			}

			if (smallest == index) {
				break;
			}
			swap(array, smallest, index);
			index = smallest;
		}
	}

	public Item extractMin() {
		Item min = getMin();
		swap(array, 1, size);
		array[size--] = null;
		siftdown(1);
		return min;
	}

	public Item getMin() {
		return array[1];
	}

	public void delete(Item item) {
		int i = 1;
		for (i = 1; i <= size; i++) {
			if (array[i] == item) {
				swap(array, i, size);
				array[size--] = null;
				siftdown(i);
				break;
			}
		}
	}

	public int size() {
		return size;
	}

	@SuppressWarnings("unchecked")
	public static void main(String args[]){

		Integer arrA [] = {3,2,1,7,8,4,10,16,12};
		System.out.println("Original Array : ");
		for(int i = 0; i<arrA.length; i++){
			System.out.print("  " + arrA[i]);
		}
		System.out.println();

		@SuppressWarnings("rawtypes")
		minheap heap = new minheap(arrA.length);
		System.out.print("\n Min-Heap : ");
		heap.createHeap(arrA);
		heap.display();

		System.out.print("Extract Min :");
		for(int i=0; i < arrA.length; i++){
			System.out.print("  " + heap.extractMin());
			System.out.print("\n Min-Heap : ");
			heap.display();
		}

	}
}

```
