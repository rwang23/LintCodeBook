##Iterator
```java
    public static void main(String []argh)
    {
        ArrayList mylist = new ArrayList();
        mylist.add("Hello");
        mylist.add("Java");
        mylist.add("4");
        Iterator it=mylist.iterator();
        while(it.hasNext())
        {
            Object element = it.next();
            System.out.println((String)element);
        }
    }
```
####Problems
[Source](http://www.javacodegeeks.com/2011/05/avoid-concurrentmodificationexception.html)
Java Collection classes are fail-fast which means that if the Collection will be changed while some thread is traversing over it using iterator, the iterator.next() will throw a ConcurrentModificationException.
This situation can come in case of multithreaded as well as single threaded environment.
Lets explore this scenario with the following example:

```java
Map<Integer, String> hashMap = new HashMap<Integer, String>(5);
    hashMap.put(1, "apple");
    hashMap.put(2, null);
    hashMap.put(new Integer(3), "peach");
    hashMap.put(3, "orange");
    hashMap.put(4, "peach");

    for (String v : hashMap.values()) {

        if ("orange".equals(v)) {
            hashMap.put(5, "banana");
        }
    }
    System.out.println(hashMap.get(5));
```

####To Avoid ConcurrentModificationException in multi-threaded environment:
1. You can convert the list to an array and then iterate on the array. This approach works well for small or medium size list but if the list is large then it will affect the performance a lot.
2. You can lock the list while iterating by putting it in a synchronized block. This approach is not recommended because it will cease the benefits of multithreading.
3. If you are using JDK1.5 or higher then you can use ConcurrentHashMap and CopyOnWriteArrayList classes. It is the recommended approach.

####To Avoid ConcurrentModificationException in single-threaded environment:
You can use the iterator remove() function to remove the object from underlying collection object. But in this case you can remove the same object and not any other object from the list.
