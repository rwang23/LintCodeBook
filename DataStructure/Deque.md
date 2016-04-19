##Deque

可以理解为stack + queue

Deque deque = new LinkedList<>();



可以从头进,从头出,从尾进,从尾出

      peek()
      Retrieves, but does not remove, the head of the queue represented by this deque, or returns null if this deque is empty.

      pop()
      Pops an element from the stack represented by this deque.

      push(E e)
      Pushes an element onto the stack represented by this deque.

      addFirst(E e)
      Inserts the specified element at the front of this deque.

      addLast(E e)
      Inserts the specified element at the end of this deque

      getFirst()
      Retrieves, but does not remove, the first element of this deque.

      getLast()
      Retrieves, but does not remove, the last element of this deque.

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
