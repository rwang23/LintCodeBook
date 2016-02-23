#Design Pattern
[Design pattern from programmer interview](http://www.programmerinterview.com/index.php/design-pattern-questions/design-pattern-interview-question-1/)


###Suppose you have a logger class that is used to log error and warning messages. How can you implement this class while using the Singleton design pattern?

The Singleton design pattern – when applied to a given class – basically limits the class itself to having just one instance created.

So, if we want to implement the Singleton design pattern with a logger class, it means that there can be at most one instance of the logger class. How can we accomplish this? First, let’s rephrase that question into something more specific to the problem at hand – how can we control the initialization of a class? Well, through the constructor of course.

A private constructor is key to the Singleton

More specifically, if we make the constructor private, this means that no one outside of the class can create an instance of the class. So, the one and only instance of the class will be created within the logger class itself, and not outside of the logger class.

Now, here is what the Java code for our Logging class would look like:

Example of Singleton in Java

```java
// Implements a simple logging class using a singleton.
	public class Logging {

	// this creates the actual Singleton instance
	private static final Logging singletonInstance =
	new Logging();

	/* Private constructor prevents others from
	   instantiating this class: */
	private Logging()
	{
	}

	// this method returns the singleton instance
	public static Logging getSingleton()
	{
	  return singletonInstance;
	}

	/* This will print a message to the screen:
	   sample call: Logging.getSingleton().log("testing message");
	*/

	public void log( String message )
	{
	  System.out.println( System.currentTimeMillis()
	  + ": " + message );
	}
}
```

###Suppose you have an application that uses the Singleton Design pattern for one of it’s classes. But, the problem is that the singleton is expensive to create, because a resource intensive database access is necessary to create the singleton. What can you do to possibly add some efficiency to the process of creating a singleton?

This question is part 2 in our series of design interview questions. It will help if you read part 1 first, since we refer to some of the code that’s used in part 1.

So, the question here is what can you do to help a situation in which a Singleton is expensive to create.

The Singleton design pattern says that there can only be one instance of the class to which the pattern is applied. But, the Singleton design pattern does not say anything at all about when exactly that instance must be created.

Create the instance right before it is needed

Let’s use the Logging class example that we went through in part 1 – you can just assume that creating the singleton for the Logging class is very resource intensive.
So, instead of creating an instance of the Logging class when the class is loaded, we will just create the instance right before that instance is actually needed.

This means that we will need to change the getSingleton() method to initialize the instance of the Logging class, but only if that instance has not been initialized already. So, the new getSingleton() method would now look like this – where singletonInstance represents the instance of the singleton of course:

```java

public static Logging getSingleton() {
/*Create the singleton instance only if it's
  null, which means no one else has created it
  already
*/
             if( singletonInstance  == null ){
                 singletonInstance  = new Logging();
             }

             return singletonInstance;
         }
```

Just for reference, this is what the getSingleton() method looked like before – note that the singletonInstance is not being initialized:

```java
public static Logging getSingleton()
{
  return singletonInstance;
}

```

And the singleton itself will be changed to look like this:

	/* note that it is no longer final and it initially points to null
	   the old version looked like this - because it was initialized
	   without anyone actually calling the getSingleton method :
	   private static final Logging singletonInstance = new Logging();
	*/
private static Logging singletonInstance = null;
Note that the method used to retrieve the Singleton instance will now check to see if the “instance” member variable is null. If it is null that of course means that the singleton has not yet been created, so it will then actually create the instance. This will of course only happen the first time the getInstance method is called. But if instance is not null, the instance will simply be returned.

This technique is known as lazy loading

So, we want to repeat that the key thing to understand here is that the method has been changed to check if an instance already exists. If it does exist, it just returns that instance. If it doesn’t exist, then it just creates a new instance and returns that one. The whole point of this is to save resources by instantiating the Singleton only when it’s actually needed. This technique is commonly known as lazy loading, or deferred initialization, because of the fact that the singleton instance is created only once it’s needed – hence it’s “lazy” or “deferred”.

##When using the Observer pattern, what approaches can be used by the subject so that it’s observers can be more efficiently updated?

Let’s go through a quick overview of the Observer pattern before answering the actual question.

In the Observer pattern, an object can broadcast any changes in it’s state to any “observers” – which are basically other classes – that want to know about it’s state. Why would an “observer” be interested in another object’s state? Well, because the state of the object can affect the state of the observer – read below for an actual example. So, the object being observed is called the “subject”. These observers are typically notified when the subject changes because the subject will call a method belonging to an observer.

###Observer Pattern is used in MVC

The Observer pattern plays a key role in the popular MVC – Model View Controller – architectural pattern. Any change in state to the Model – which represents the underlying data, and is the “subject” – will result in a notification to the View, which is the Observer.

Now, let’s answer the actual question. One problem that may arise with the Observer pattern is that a subject may be updating it’s state too frequently. This means that the subject is spending a great deal of time updating it’s observers, which is of course inefficient. In this scenario, a possible solution is to simply have the subject turn off all updates temporarily. Then, the subject can make the changes in that period of time. And, once the changes are complete, the subject can go ahead and update any and all observers with one big notification. This is far more efficient because of the fact that only notification is sent out to observers as opposed to constantly sending out notifications.

###Finding a good strategy with the Observer Pattern

One other possible dilemma when dealing with the Observer pattern is figuring out a good strategy for observers to know what has been changed in the subject. Let’s consider an example website (like Yahoo.com) that has to update particular parts of the page (the Observer) when the data (the subject) changes. So when a stock price changes, Yahoo will have to update the stock portion of the page, and if there’s some breaking news, then Yahoo will have to update the “Latest News” portion of the page, etc.

In order for this process to be efficient, the Observer (which is the actual webpage) would need to know what data (the subject) has changed – whether that data is in the form of a database, XML file, or whatever. But, instead of having the page ask the data (or query the data) to find out what exactly has changed, it would probably be more efficient to have the data (the subject) pass on that information to the webpage. This information passed to the webpage from the subject could just be added to the normal update notification, and then the webpage can update the appropriate portion of the page that needs to change (maybe using AJAX).

##When and why would you favor the Decorator pattern over inheritance?

Just a quick note: even if you don’t know much about the Decorator pattern, you should still be able to understand the discussion here.

The Decorator design pattern is used to wrap one object with another object. The point of wrapping one object with another object is so that the original object’s behavior can be modified.

The wrapper object can be used as a substitute for the original object because of the fact that both objects either share the same abstract class or implement the same interface.

###Inheritance vs the Decorator Pattern

The thing that both inheritance and the decorator pattern have in common is the fact that they both allow you to change how an object behaves. But how they achieve this change in behavior is where inheritance and the decorator pattern are different.

###The Decorator pattern makes run-time object changes easier

With inheritance, dynamically changing the behavior of an object can be a burdensome process. Suppose that you want to dynamically change the behavior of an object using inheritance. Since we are dealing with inheritance, you will need to use a child class and then create an object of that child class in order to get the desired effect. After you create the child class object you will then need to copy the state from the current object into the new child class object – because you will presumably want to still save the state of the current object. And finally, after you are done copying the state, you will want to discard the old object since you no longer need it. This is obviously a long process that can be quite a pain to implement over and over again.

But if we use the Decorator pattern instead, it is a lot easier to dynamically change the behavior of the object. All we have to do is wrap the current object with another object that contains the extra behavior that is desired.

###The Decorator Pattern makes multiple behavior modifications easier

Suppose that you have many different changes that you would like to implement for a given class. And, also assume that those changes do not conflict with one another, so you can combine those modifications in any order without having to worry about potential conflicts. In this scenario, using the Decorator pattern can be very advantageous over inheritance. Let’s go over an example to understand this concept further.

As our example, let’s say that we have a Car class. This class could have many different behaviors like Automatic, Manual, Convertible, etc. We could have these behaviors implemented using inheritance. So, we could create classes called AutomaticCar, ManualCar, or ConvertibleCar that all derive from the Car class. While this is just fine for a reasonable number of child classes, for more behaviors (like LuxuryCar, SedanCar, etc) this process of creating more and more child classes can quickly become very messy. But, by using the Decorator pattern instead of inheritance, we can avoid this problem of having far too many child classes. This is because with the Decorator pattern, each and every behavior is described by just one Decorator class. And, you can specify whatever behaviors you want by applying the desired set of decorations.

###The Decorator pattern is not necessary in non-dynamic situations

Using the Decorator pattern is pretty darn complex. If you actually need to dynamically change the way an object behaves, then using the Decorator pattern is a good idea. But, if you do not need to dynamically change the way an object behaves, then inheritance is the better option because you then do not need to deal with the complexity of the Decorator patter

##How would you implement thread safety in a singleton?

First, let’s go over some background on why thread safety may be an issue with singletons. When dealing with singletons, there are two primary ways to initialize the singleton – inside a method using a technique known as lazy loading, or outside a method. Lazy loading is used to save resources by only initializing the singleton when the instance is actually needed. This is what lazy loading could look like for a singleton:

```java
public static Logging getSingleton() {
  /*Create the singleton instance only if it's
    null, which means no one else has created it
    already:
   */

   if( singletonInstance  == null ){
      singletonInstance  = new Logging();
   }

   return singletonInstance;
}
```
Just for reference, this is what the getSingleton() method looks like without lazy loading – note that the singletonInstance is not being initialized:

```java
public static Logging getSingleton()
{
  return singletonInstance;
}
```
You can read more about lazy loading in Singletons here: Design Pattern Interview Question 2.

##Having the singleton initialized in a method can be a problem

Having the singleton initialized inside a method creates a new problem. What if two or more threads call the method at the same time?


For example, let’s say that a thread – let’s call it thread A – switches out immediately after checking to see if the singleton instance is NULL. Now, let’s say that another thread – call it thread B – gets switched into the method call and actually completes the execution of the getInstance() method. This means that thread B will actually retrieve and construct an instance of the singleton. But, thread A will get switched back into the method and then create another instance of the singleton! So, now we have two singleton instances, when the whole point of a singleton is to only allow one instance to be created.

##Make the singleton thread safe is the solution

This is clearly a problem, but there is a solution. That solution is to make the method thread safe. How do we make a method thread safe? Well, it’s pretty simple actually – we just add the synchronized keyword to the method signature to make it thread safe. So, this is what the method ends up looking like:

```java
// Return the singleton instance.
     public synchronized static Logger getInstance() {
         if( instance == null ){
             instance = new Logger();
         }

         return instance;
     }
```

##How does the synchronized keyword make a method thread safe?

Adding the synchronized keyword to the method signature basically prevents more than one thread from entering the method at a given time. So, one thread must run the method to completion before another thread can even enter the method. This will of course prevent multiple singletons from being created because once the first singleton is created, any subsequent calls to the getInstance method will just return the one instance that has already been created. And that is what thread safety is all about.
