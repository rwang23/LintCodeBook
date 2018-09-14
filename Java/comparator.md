##Comparator用法


####Compare
- 是比较两个Object是否相同的办法,需要overwrite hashCode()
- list1.equals(list2), 这个如果元素相等的话,是相等的,虽然两个list内存地址不同

  	From the javadoc:

  	Compares the specified object with this list for equality. Returns true if and only if the specified object is also a list, both lists have the same size, and all corresponding pairs of elements in the two lists are equal.

####CompareTo

    a compareTo() method that will define the order of two instances of a given object. Specifically, our compareTo() method needs to return an integer as follows:

    a negative number if our object comes before the one passed in; -1 表明 从小到大
    a positive number if our object comes after the one passed in; +1 表明 从大到小
    otherwise, zero (meaning they're equal in terms of ordering).


####Comparator
Comparator 不能直接用在char int上边,要用在Character Integer,否则就要报错

```java
public class Solution {
    /**
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] input) {
        //write your code here
        Character[] temp = new Character[input.length];
        for (int i = 0; i < input.length; i++) {
            temp[i] = input[i];
        }
        //Arrays.sort(temp, new letterComparator<Character>());
        Arrays.sort(temp, new Comparator<Character>() {
            public int compare(Character c1, Character c2) {
              int i1 = c1 >= 'a' ? (int)c1 - 'a' : (int)c1;
              int i2 = c2 >= 'a' ? (int)c2 - 'a' : (int)c2;
              return i1 - i2;
            }
        });
        for (int i = 0; i < input.length; i++) {
            input[i] = temp[i];
        }
    }

}

```

```java
public class Solution {
    /**
     *@param chars: The letter array you should sort by Case
     *@return: void
     */
    public void sortLetters(char[] input) {
        //write your code here
        Character[] temp = new Character[input.length];
        for (int i = 0; i < input.length; i++) {
            temp[i] = input[i];
        }
        //Arrays.sort(temp, new letterComparator<Character>());
        Arrays.sort(temp, new letterComparator());
        for (int i = 0; i < input.length; i++) {
            input[i] = temp[i];
        }
    }

    public class letterComparator implements Comparator<Character> {
        public int compare(Character c1, Character c2) {
            int i1 = c1 >= 'a' ? (int)c1 - 'a' : (int)c1;
            int i2 = c2 >= 'a' ? (int)c2 - 'a' : (int)c2;
            return i1 - i2;
        }
    }
}

```




```java
import java.util.*;

class Dog implements Comparator<Dog>, Comparable<Dog>{
   private String name;
   private int age;
   Dog(){
   }

   Dog(String n, int a){
      name = n;
      age = a;
   }

   public String getDogName(){
      return name;
   }

   public int getDogAge(){
      return age;
   }

   // Overriding the compareTo method
   public int compareTo(Dog d){
      return (this.name).compareTo(d.name);
   }

   // Overriding the compare method to sort the age
   public int compare(Dog d, Dog d1){
      return d.age - d1.age;
   }
}

public class Example{

   public static void main(String args[]){
      // Takes a list o Dog objects
      List<Dog> list = new ArrayList<Dog>();

      list.add(new Dog("Shaggy",3));
      list.add(new Dog("Lacy",2));
      list.add(new Dog("Roger",10));
      list.add(new Dog("Tommy",4));
      list.add(new Dog("Tammy",1));
      Collections.sort(list);// Sorts the array list

      for(Dog a: list)//printing the sorted list of names
         System.out.print(a.getDogName() + ", ");

      // Sorts the array list using comparator
      Collections.sort(list, new Dog());
      System.out.println(" ");
      for(Dog a: list)//printing the sorted list of ages
         System.out.print(a.getDogName() +"  : "+
		 a.getDogAge() + ", ");
   }
}
```
