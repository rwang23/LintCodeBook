##Gabage Collection
- System class contains a static method
- System.gc();

##By Runtime class
- Runtime r = Runtime.getRuntime();
- freeMemory() // return freemomory in the heap
- totalMemory() // return total of the heap
- gc() for requesting jvm to run garbage collector
- when object is no use, when we call gc, we automatically call this object finaliza method
- this object finallize

```java
class C {
	C i;
   public static void main(String[] args) {
	   C t = new C();
	   t = null;
	   System.gc();
	   System.out.println("end of main");
   }

   public void finalize() {
	   System.out.println("finalize method");
	   System.out.println(10 / 0);// will ignore when runtime
   }
}

// finalize method
// end of main

```
