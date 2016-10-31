####abstract class vs interface
- Interface in Java can only contains declaration. You can not declare any concrete methods inside interface. On the other hand abstract class may contain both abstract and concrete methods, which makes abstract class an ideal place to provide common or default functionality.
- You can implement multiple interface but can only extends one abstract, Which means interface can provide more Polymorphism support than abstract class .
- In order to implement interface in Java, you need to provide implementation of all methods, which is very painful. On the other hand abstract class may help you in this case by providing default implementation.

####interface
- we can creat object of abstract and interface
- X b = new A();
- X is interface and A is the class implement the X

```java
//we can creat object of abstract and interface using anonymous block
interface X
{
	//bydefault interface varibles are constants
	int i=100;
	//by default interface methods are abstract
	void funX();
}

class A {
	X x=new X() {
		public void funX(){
			System.out.println("inside funX");
		}
	}; // this : is important
	public static void main(String[] args) {
		A b=new A();
		b.x.funX();//important
	}
}

```

```java
class A {
	interface X {
		void funcA() {

		}
	}
}

class B {
	A.X a = new A.X {
		void funcA() {

		}
	};
}
```
#####inside the class we can define a interface
- 另一个小点: 两个interface可以extend

```java
class B {
	interface X {
		void funX();
	}
	interface Y extends X { //两个interface可以extend
		void funY();
	}
	int i=100;
	void funB() {
	System.out.println("inside funB");
	}
}

class A implements B.Y {
	public void funX() {
		System.out.println("Inside funX");
	}
	public void funY() {
		System.out.println("Inside funY");
	}

	public static void main(String[] args) {
		A b=new A();
		b.funX();
		b.funY();
		System.out.println("Hello World!");
	}
}
```

#####如果一个class里边含有interface,那么扩展他的class不需要扩展这个interface
- 下面的这个例子,可以不需要implement funX,除非声明是 class A extends B implements  B.X,就必须

```java
class B {
	interface X {
		void funX();
	}
	void funB() {
		System.out.println("inside funB");
	}
}


class A extends B {
	public void funX() { // 不implement 这个funX也可以运行
		System.out.println("Inside funX");
	}
	public void funY() {
		System.out.println("Inside funY");
	}

	public static void main(String[] args) {
		A b=new A();
		b.funX();
		b.funY();
		System.out.println("Hello World!");
	}
}
```

