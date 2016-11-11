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
//InnerClass Supports Inheritance
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
####在static innerclass里边 只能声明static method和static variable

####LocalInnerclass
- if we declare a class inside the methods is called as localinnerclass.
- localinnerclass will not support private ,protected static keyword
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
