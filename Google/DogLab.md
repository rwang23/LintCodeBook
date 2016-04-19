##Dog Lab
A lab is doing some gene disease research on dogs. Like people, they give each dog a name and record dogs' family hierarchies like below. (dad,mom).
Given two dogs, can you help to find out if they are blood related?

true   --  Camo and Adele
true   --  Cali and Abi
false  --  Bain and Edee


           (Cacho,Abi)           (Baci,Ada)

           /     |    \         /    |     \
    (Abby,Echo) Cali  (Dagger,Ada)  Adole  (Devo,Adele)
         /                 |                  \
      Bain                Camo                Edee


####思路
- DFS
- Union-Find
- level order traversal

```java
public Class Dog
{
    private String name;
    private int age;
    private Dog[] children;
    private Dog dad;
    private Dog mom;
    Dog(String name) {
        this.name = name;
    }
}

bool areBloodRelated(Dog a, Dog b)
{
    Set<Dog> set = new HashSet<Dog>();
    Dog cur = a;
    Queue<Dog> queue = new LinkedList<Dog>();
    queue.offer(a);
    while (!queue.isEmpty()) {
        cur = queue.poll();
        set.add(cur);
        if (cur.dad != null) {
            queue.offer(cur.dad);
        }
        if (cur.mom != null) {
            queue.offer(cur.mom);
        }
    }

    queue.offer(b);
    while (!queue.isEmpty()) {
        cur = queue.poll();
        if (set.contains(cur)) {
            return true;
        }
        if (cur.dad != null) {
            queue.offer(cur.dad);
        }
        if (cur.mom != null) {
            queue.offer(cur.mom);
        }
    }
    return false;
}

```
