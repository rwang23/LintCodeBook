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
