##Objects and Classes
Java is an Object-Oriented Language.
As a language that has the Object Oriented feature, Java supports the following fundamental concepts:

	Polymorphism
	Inheritance
	Encapsulation
	Abstraction
	Classes
	Objects
	Instance
	Method
	Message Parsing

###modifiers
- public: can access any
- protected: subclass, same class, same package (subclass可能不在一个package)(not protected)
- package: same class, same package(没有subclass了)
- private: same class


###Reference vs Object Type
```java
Person p = new Student();
//能这么使用因为 is a
//但是 Student s = new Person()
//就错了, person 不一定是student
student is a person
Person[] p = new Person[3];
p[0] = new Person();
p[1] = new Student();
p[2] = new Faculty();
```
###Object Creation
Student s = new Student();
先initilize了Object,然后initialize了person,最后才是student

```java
public class Person {
	private String name;
}
//其实是compiler已经帮我们做好了一些工作了,已经变成了下面这样了
public class Person extends Object {
	private String name;
	public Person() {
		super();
		//super() has to be the first line
	}
}
```
```java
public class Person extends Object {
	private String name;
	public Person(String n) {
		super();
		this.name = n;
	}
}

public class Student extends Person {
	public Student(String n) {
		super();
		//this.name = n; 这样写就出问题了,因为name是person的private的,不能这么去access
		super(n);//要这么去access
	}
}
```

