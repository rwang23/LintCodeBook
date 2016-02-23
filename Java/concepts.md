##OverLoading

	public int distance(double a, double b)
	public double distance(double a, double b)
	是不合法的,不能这样overload
	除非parameter list也是不同的

##Public vs Private
###For variable
	private means only accessable within class
	so that we can use getter and setter, giving us more control
###For functions


###Volatile
The Java volatile keyword is used to mark a Java variable as "being stored in main memory". More precisely that means, that every read of a volatile variable will be read from the computer's main memory, and not from the CPU cache, and that every write to a volatile variable will be written to main memory, and not just to the CPU cache.
[Example from StackOverFlow](http://stackoverflow.com/questions/9749746/what-is-the-difference-between-atomic-volatile-synchronized)
###Static
Static variables belong to a class and not to any individual instance.
Read more at http://javabeginnerstutorial.com/core-java-tutorial/transient-vs-static-variable-java/#dK94E1k8lt1lQVEG.99
###Transient
[Transient](http://www.javabeat.net/what-is-transient-keyword-in-java/)

####Serialization
Serialization is the process of making the object’s state is persistent. That means the state of the object is converted into stream of bytes and stored in a file. In the same way we can use the de-serilization concept to bring back the object’s state from bytes. This is one of the important concept in Java programming because this serialization is mostly used in the networking programming. The object’s which are needs to be transmitted through network has to be converted as bytes, for that purpose every class or interface must implement  serialization interface. It is a marker interface without any methods.

####Transient
The keyword transient in Java used to indicate that the variable should not be serialized. By default all the variables in the object is converted to persistent state. In some cases, you may want to avoid persisting some variables because you don’t have the necessity to transfer across the network. So, you can declare those variables as transient. If the variable is declared as transient, then it will not be persisted. It is the main purpose of the transient keyword.

####Example
```java
package javabeat.samples;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class NameStore implements Serializable{
	private String firstName;
	private transient String middleName;
	private String lastName;
	public NameStore (String fName,
                         String mName,
                         String lName){
		this.firstName = fName;
		this.middleName = mName;
		this.lastName = lName;
	}
	public String toString(){
		StringBuffer sb = new StringBuffer(40);
		sb.append("First Name : ");
		sb.append(this.firstName);
		sb.append("Middle Name : ");
		sb.append(this.middleName);
		sb.append("Last Name : ");
		sb.append(this.lastName);
		return sb.toString();
	}
}
public class TransientExample{
	public static void main(String args[]) throws Exception {
		NameStore nameStore = new NameStore("Steve",
                                     "Middle","Jobs");
		ObjectOutputStream o = new ObjectOutputStream
                   (new FileOutputStream("nameStore"));
		// writing to object
		o.writeObject(nameStore);
		o.close();

		// reading from object
		ObjectInputStream in =new ObjectInputStream(
                new FileInputStream("nameStore"));
		NameStore nameStore1 = (NameStore)in.readObject();
		System.out.println(nameStore1);
	}
}
// output will be :
First Name : Steve
Middle Name : null
Last Name : Jobs
```
static will not be saved either
