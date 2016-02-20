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
		super();//这行不写也是强制执行的
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
	public void setName(String n) {
		this.name = n;
	}
}

public class Student extends Person {
	public Student(String n) {
		super();
		//this.name = n; 这样写就出问题了,因为name是person的private的,不能这么去access
		super(n);//要这么去access
	}
	public Student() {
		this("student");//这种方式也能Initialize,调用了上面的initialize的方式
	}
}

public class Faculty extends Person {
	public Faculty(String n) {
		this.setName("student");
		//这样写,一定会出现compiler error
		//因为compiler会自动先加上一句super()
		//然而在person里边,没有没有添加参数的constructor,所以compiler error
	}

}

```

###Overriding
####Overloading vs Overriding
- Overloading: same class has same method name with different parameters
- Overriding: subclass has same method name with the same parameters as the superclass

```java
public class Person {
	private String name;
	public String toString() {
		return this.getName();
	}
}
```

###Polymorphism

		Person
		String name
		String getName()
		String toString()

		Student
		int studentID
		int getId()
		String toString()

```java
Person s = new Student("cara", 1234);
//s.getId()
//如果按照上边这么写,  compiler error
//因为compiler不知道在调用的是student的,它只去person里边找了
//这个时候就要用casting了
((Student) s).getId();
//这样写才行,告诉compiler 相信自己的代码
//但是这样如果s不是student,就会出现runtime error
```
有更好的办法

```java
if (s instanceof Student) {
	((Student) s).getId();
}
```
	Person s = new Student("cara", 1234);
	如果之后s调用了function,
	是哪个class的就调用哪个class里边的function
	所以s调用的是student
	哪怕student和Person都有的function,也是按照student的标准调用
	如果子类里边没有,就调用父类里边的(如果里边出现了this,this指的现在的s)



	// Assume the variable feature stores a PointFeature object
	SimplePointMarker pm = new OceanQuakeMarker(feature);
	EarthquakeMarker em = pm;
	Sorry, that's incorrect.
	The first line is fine. But the second line will not work without a cast. Even though the object pointed to by pm is actually an OceanQuakeMarker, which is always an EarthquakeMarker, java "forgets" about that. To fix the problem, you can change the second line to:

	EarthquakeMarker em = (EarthquakeMarker)pm;

###Abstract and Interface

Interface only define required methods

class must be abstract if any methods are
(indicate methods have to be modified)

