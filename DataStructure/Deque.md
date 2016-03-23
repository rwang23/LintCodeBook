##Deque

可以理解为stack + queue

Deque deque = new LinkedList<>();



可以从头进,从头出,从尾进,从尾出

	addFirst()
	removeFirst() = poll()
	addLast()
	removeLast()
	getFirst() = peek()
	getLast()
	size()

```java
   deque.add(15);
   deque.add(30);
   deque.add(20);
   deque.add(18);

   // let us print all the elements available in deque
   for (Integer number : deque) {
   System.out.println("Number = " + number);
   }

   // getFirst() will retrieve element at first(head) position
   int retval = deque.getFirst();
   System.out.println("Retrieved Element is = " + retval);

```
```
Number = 15
Number = 30
Number = 20
Number = 18
Retrieved Element is = 15
```
