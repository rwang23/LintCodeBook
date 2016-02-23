#Design Pattern
Suppose you have a logger class that is used to log error and warning messages. How can you implement this class while using the Singleton design pattern?

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
