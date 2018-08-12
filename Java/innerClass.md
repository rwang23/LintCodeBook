####注意41行,innerclass的创建

```java
class B {
	int k = 900;
	static int f = 180;
}

interface X {
	int l = 658;
}

class A {
	int i=100;
	static int j=200;
//Inner class supoorts Interfaces
//InnerClass Supports Inheritance but only one class and one interface
//Innerclass supports Accespecifiers(private,public,default,protected)
	private	class Inner extends B implements X {
	//Static varibles and methods we cannot declare inside the non-Static innerclass but if u declare final keyword before static varibles and methods we can declare inside the non-Static innerclass
	//Non-Static varibles and methods and Static varibles and methods of outer class we can access Directly from non-Static innerclass
		final static int m = 600;
		void funIn() {
			System.out.println(l);//658
			System.out.println(k);//900
			System.out.println(f);//180
			System.out.println(i);//100
			System.out.println(j);//200
			System.out.println("inside funin");
		}//innerclassmethod
	}//non-static innerclass

	void funOu() {
//here we can create object innerclass directly
		Inner d=new Inner();
		System.out.println(d.m);

	}//Outerclass methods
	public static void main(String[] args) {
		//We cannot create object of innerclass Directly for eg: Inner i=new Inner();
		A.Inner b = new A().new Inner();
		b.funIn();
		A   c = new A();
		c.funOu();
		System.out.println("Hello World!");
	}
}
```
####LocalInnerclass
- if we declare a class inside the methods is called as localinnerclass.
- localinnerclass will not support private ,protected, static keyword
- localinner class support inheritance and inteface,abstracts..

```java
class A {
	//if we declare inside the methods class is called as localinnerclass.
	void funA() {
		class LocalIn {
	//we cannot create object of localinnerclass out side class main method
			void funIn() {
				System.out.println("inside funIn");
			}
		}//localinnerclass

		LocalIn l = new LocalIn();
		l.funIn();
	}

	public static void main(String[] args) {
		A b = new A();
		b.funA();
		System.out.println("Hello World!");
	}
}
```
```
Which is true about a method-local inner class?
A.	It must be marked final.
B.	It can be marked abstract.
C.	It can be marked public.
D.	It can be marked static.
Answer: Option B

Explanation:

Option B is correct because a method-local inner class can be abstract, although it means a subclass of the inner class must be created if the abstract class is to be used (so an abstract method-local inner class is probably not useful).

Option A is incorrect because a method-local inner class does not have to be declared final (although it is legal to do so).

C and D are incorrect because a method-local inner class cannot be made public (remember-you cannot mark any local variables as public), or static.
```

```
public class MyOuter
{
    public static class MyInner
    {
        public static void foo() { }
    }
}
which statement, if placed in a class other than MyOuter or MyInner, instantiates an instance of the nested class?
A.	MyOuter.MyInner m = new MyOuter.MyInner();
B.	MyOuter.MyInner mi = new MyInner();
C.
MyOuter m = new MyOuter();
MyOuter.MyInner mi = m.new MyOuter.MyInner();
D.	MyInner mi = new MyOuter.MyInner();
Answer: Option A

Explanation:

MyInner is a static nested class, so it must be instantiated using the fully-scoped name of MyOuter.MyInner.

Option B is incorrect because it doesn't use the enclosing name in the new.

Option C is incorrect because it uses incorrect syntax. When you instantiate a nested class by invoking new on an instance of the enclosing class, you do not use the enclosing name. The difference between Option A and C is that Option C is calling new on an instance of the enclosing class rather than just new by itself.

Option D is incorrect because it doesn't use the enclosing class name in the variable declaration.
```
