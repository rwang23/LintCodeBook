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
