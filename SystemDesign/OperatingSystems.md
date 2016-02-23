#Operating Systems
[From ProgrammerInterview.com](http://www.programmerinterview.com/index.php/operating-systems/how-virtual-memory-works/)

##What is virtual memory, how is it implemented, and why do operating systems use it?

Real, or physical, memory exists on RAM chips inside the computer. Virtual memory, as its name suggests, doesn’t physically exist on a memory chip. It is an optimization technique and is implemented by the operating system in order to give an application program the impression that it has more memory than actually exists. Virtual memory is implemented by various operating systems such as Windows, Mac OS X, and Linux.

So how does virtual memory work? Let’s say that an operating system needs 120 MB of memory in order to hold all the running programs, but there’s currently only 50 MB of available physical memory stored on the RAM chips. The operating system will then set up 120 MB of virtual memory, and will use a program called the virtual memory manager (VMM) to manage that 120 MB. The VMM will create a file on the hard disk that is 70 MB (120 – 50) in size to account for the extra memory that’s needed. The O.S. will now proceed to address memory as if there were actually 120 MB of real memory stored on the RAM, even though there’s really only 50 MB. So, to the O.S., it now appears as if the full 120 MB actually exists. It is the responsibility of the VMM to deal with the fact that there is only 50 MB of real memory.

##The paging file and the RAM


Now, how does the VMM function? As mentioned before, the VMM creates a file on the hard disk that holds the extra memory that is needed by the O.S., which in our case is 70 MB in size. This file is called a paging file (also known as a swap file), and plays an important role in virtual memory. The paging file combined with the RAM accounts for all of the memory. Whenever the O.S. needs a ‘block’ of memory that’s not in the real (RAM) memory, the VMM takes a block from the real memory that hasn’t been used recently, writes it to the paging file, and then reads the block of memory that the O.S. needs from the paging file. The VMM then takes the block of memory from the paging file, and moves it into the real memory – in place of the old block. This process is called swapping (also known as paging), and the blocks of memory that are swapped are called pages. The group of pages that currently exist in RAM, and that are dedicated to a specific process, is known as the working set for that process.

As mentioned earlier, virtual memory allows us to make an application program think that it has more memory than actually exists. There are two reasons why one would want this: the first is to allow the use of programs that are too big to physically fit in memory. The other reason is to allow for multitasking – multiple programs running at once. Before virtual memory existed, a word processor, e-mail program, and browser couldn’t be run at the same time unless there was enough memory to hold all three programs at once. This would mean that one would have to close one program in order to run the other, but now with virtual memory, multitasking is possible even when there is not enough memory to hold all executing programs at once.

##Virtual Memory Can Slow Down Performance

However, virtual memory can slow down performance. If the size of virtual memory is quite large in comparison to the real memory, then more swapping to and from the hard disk will occur as a result. Accessing the hard disk is far slower than using system memory. Using too many programs at once in a system with an insufficient amount of RAM results in constant disk swapping – also called thrashing, which can really slow down a system’s performance.

##Paging and Page Faults

Suppose we have a paging system with 4 frames and 12 pages, where the number of frames denotes the number of pages that can be held in RAM at any given time. Assume the pages are accessed by some program in the order shown below, from left to right. Also, assume that the program has just started, so the frames are initially empty. How many page faults will be generated assuming that the LRU (Least Recently Used) algorithm is being used?


Order in which pages are accessed:
3, 4, 2, 1, 4, 7, 2, 5, 3, 6, 1, 3

Reading the previous discussion on virtual memory is recommended to better understand this problem. `A page fault occurs when a program tries to access a page that is mapped in address space, but not loaded in the physical memory (the RAM).` In other words, a page fault occurs when a program can not find a page that it’s looking for in the physical memory, which means that the program would have to access the paging file (which resides on the hard disk) to retrieve the desired page.

The term page fault is a bit misleading as it implies that something went seriously wrong. Although page faults are undesirable – as they result in slow accesses to the hard disk – they are quite common in any operating system that uses virtual memory.


Now, we need to actually solve the problem. The easiest way to do this is to break the problem down into 12 steps (where 12 is the number of pages) to see what happens each time a page is referenced by the program, and at each step see whether a page fault is generated or not. Of course, we want to keep track of what pages are currently in the physical memory (the RAM). `The first four page accesses will result in page faults because the frames are initially empty.` After that, if the program tries to access a page that’s already in one of the frames then there’s no problem. But if the page that the program is trying to access is not already in one of the frames then that results in a page fault. In this case, we have to determine which page we want to take out (or ‘swap’) from the RAM, and for that we use the LRU algorithm.

Some other algorithm could be used as well – FIFO and NRU are other possibilities – and as a group these are known as page replacement algorithms. Applying the LRU algorithm to this problem is fairly straightforward – you simply remove the page that was least recently used. Proceeding in this manner leads to the chart shown below – you should try this out yourself before looking at the answer.

Page referenced	Page Fault	Resulting List

			3	Y	3
			4	Y	3,4
			2	Y	3,4,2
			1	Y	3,4,2,1
			4	N	3,2,1,4
			7	Y	2,1,4,7
			2	N	1,4,7,2
			5	Y	4,7,2,5
			3	Y	7,2,5,3
			6	Y	2,5,3,6
			1	Y	5,3,6,1
			3	N	5,6,1,3

We can see that 9 page faults will be generated in this scenario.


##Swapping
###What is the purpose of swapping in virtual memory?

 Swapping is exchanging data between the hard disk and the RAM


The goal of the virtual memory technique is to make an application think that it has more memory than actually exists. If you read the recommended question then you know that the virtual memory manager (VMM) creates a file on the hard disk called a swap file. Basically, the swap file (also known as a paging file) allows the application to store any extra data that can’t be stored in the RAM – because the RAM has limited memory. `Keep in mind that an application program can only use the data when it’s actually in the RAM.` Data can be stored in the paging file on the hard disk, but it is not usable until that data is brought into the RAM. Together, the data being stored on the hard disk combined with the data being stored in the RAM comprise the entire data set needed by the application program.

So, the way virtual memory works is that whenever a piece of data needed by an application program cannot be found in the RAM, then the program knows that the data must be in the paging file on the hard disk.

But in order for the program to be able to access that data, it must transfer that data from the hard disk into the RAM. This also means that a piece of existing data in the RAM must be moved to the hard disk in order to make room for the data that it wants to bring in from the hard disk. So, you can think of this process as a trade in which an old piece of data is moved from the RAM to the hard disk in exchange for a ‘new’ piece of data to bring into the RAM from the hard disk. This trade is known as swapping or paging. Another term used for this is a ‘page fault’ – which occurs when an application program tries to access a piece of data that is not currently in the RAM, but is in the paging file on the hard disk. Remember that page faults are not desirable since they cause expensive accesses to the hard disk. Expensive in this context means that accessing the hard disk is slow and takes time.

###The Purpose Of Swapping

So, we can say that the purpose of swapping, or paging, is to access data being stored in hard disk and to bring it into the RAM so that it can be used by the application program. Remember that swapping is only necessary when that data is not already in the RAM.

###Excessive Swapping Causes Thrashing

Excessive use of swapping is called thrashing and is undesirable because it lowers overall system performance, mainly because hard drives are far slower than RAM.


##Process VS Thread
###What is the difference between a thread and a process?
###Processes vs Threads

`A process is an executing instance of an application.` What does that mean? Well, for example, when you double-click the Microsoft Word icon, you start a process that runs Word. `A thread is a path of execution within a process.` Also, a process can contain multiple threads. When you start Word, the operating system creates a process and begins executing the primary thread of that process.

It’s important to note that a thread can do anything a process can do. But since a process can consist of multiple threads, a thread could be considered a ‘lightweight’ process. Thus, `the essential difference between a thread and a process is the work that each one is used to accomplish. Threads are used for small tasks, whereas processes are used for more ‘heavyweight’ tasks – basically the execution of applications.`

Another difference between a thread and a process is that threads within the same process share the same address space, whereas different processes do not. This allows threads to read from and write to the same data structures and variables, and also facilitates communication between threads. Communication between processes – also known as IPC, or inter-process communication – is quite difficult and resource-intensive.

###MultiThreading

Threads, of course, allow for multi-threading. A common example of the advantage of multithreading is the fact that you can have a word processor that prints a document using a background thread, but at the same time another thread is running that accepts user input, so that you can type up a new document.

If we were dealing with an application that uses only one thread, then the application would only be able to do one thing at a time – so printing and responding to user input at the same time would not be possible in a single threaded application.

Each process has it’s own address space, but the threads within the same process share that address space. Threads also share any other resources within that process. This means that it’s very easy to share data amongst threads, but it’s also easy for the threads to step on each other, which can lead to bad things.

Multithreaded programs must be carefully programmed to prevent those bad things from happening. Sections of code that modify data structures shared by multiple threads are called critical sections. When a critical section is running in one thread it’s extremely important that no other thread be allowed into that critical section. This is called synchronization, which we wont get into any further over here. But, the point is that multithreading requires careful programming.

Also, context switching between threads is generally less expensive than in processes. And finally, the overhead (the cost of communication) between threads is very low relative to processes.

###Here’s a summary of the differences between threads and processes:

1. Threads are easier to create than processes since they
don't require a separate address space.

2. Multithreading requires careful programming since threads
share data strucures that should only be modified by one thread
at a time.  Unlike threads, processes don't share the same
address space.

3.  Threads are considered lightweight because they use far
less resources than processes.

4.  Processes are independent of each other.  Threads, since they
share the same address space are interdependent, so caution
must be taken so that different threads don't step on each other.
This is really another way of stating #2 above.

5.  A process can consist of multiple threads.


##What is the difference between a monitor and semaphore?

The reason that semaphores and monitors are needed is because multi-threaded applications (like Microsoft Word, Excel, etc) must control how threads access shared resources. This is known as thread synchronization – which is absolutely necessary in a multi-threaded application to ensure that threads work well with each other. If applications do not control the threads then it may result in corruption of data and other problems.

###Do I use a monitor or a semaphore?

Monitors and semaphores are both programming constructs used to accomplish thread synchronization.
Whether you use a monitor or a semaphore depends on what your language or system supports.

###What is a Monitor?

A monitor is a set of multiple routines which are protected by a mutual exclusion lock. None of the routines in the monitor can be executed by a thread until that thread acquires the lock. This means that only ONE thread can execute within the monitor at a time. Any other threads must wait for the thread that’s currently executing to give up control of the lock.

However, a thread can actually suspend itself inside a monitor and then wait for an event to occur. If this happens, then another thread is given the opportunity to enter the monitor. The thread that was suspended will eventually be notified that the event it was waiting for has now occurred, which means it can wake up and reacquire the lock.

###What is a Semaphore?

A semaphore is a simpler construct than a monitor because it’s just a lock that protects a shared resource – and not a set of routines like a monitor. The application must acquire the lock before using that shared resource protected by a semaphore.

Example of a Semaphore – a Mutex

A mutex is the most basic type of semaphore, and mutex is short for mutual exclusion. In a mutex, only one
thread can use the shared resource at a time. If another thread wants to use the shared resource, it must wait for the owning thread to release the lock.

###Differences between Monitors and Semaphores

Both Monitors and Semaphores are used for the same purpose – thread synchronization. But, monitors are simpler to use than semaphores because they handle all of the details of lock acquisition and release. An application using semaphores has to release any locks a thread has acquired when the application terminates – this must be done by the application itself. If the application does not do this, then any other thread that needs the shared resource will not be able to proceed.

Another difference when using semaphores is that every routine accessing a shared resource has to explicitly acquire a a lock before using the resource. This can be easily forgotten when coding the routines dealing with multithreading . Monitors, unlike semaphores, automatically acquire the necessary locks.

###Is there a cost to using a monitor or semaphore?

Yes, there is a cost associated with using synchronization constructs like monitors and semaphores. And, this cost is the time that is required to get the necessary locks whenever a shared resource is accessed.



##Provide an example of threading and synchronization in Java

The best way to really understand threading and the need for synchronization is through a great example. Here we will present an example of an online banking system to really help see the potential problems with multi-threading, and their solutions through the use of a thread synchronization construct like a monitor.

Let’s suppose we have an online banking system, where people can log in and access their account information. Whenever someone logs in to their account online, they receive a separate and unique thread so that different bank account holders can access the central system simultaneously.

Now let’s create a Java class to represent those individual bank accounts. Instances of this class are created when people actually log in online. Let’s name the class BankAccount. This class has a method called “deposit” that’s used to deposit funds into the bank account. This class also has another method called “transfer” to transfer funds from the bank to another account.

Here is some simple Java code that represents the BankAccount class:

```java
public class BankAccount {

    int accountNumber;

    double accountBalance;


    // to withdraw funds from the account
    public boolean transfer (double amount)
    {
        double newAccountBalance;

        if( amount > accountBalance)
	{
             //there are not enough funds in the account
             return false;
	}

	else
	{
            newAccountBalance = accountBalance - amount;
            accountBalance = newAccountBalance;
            return true;
        }

    }

    public boolean deposit(double amount)
    {
	double newAccountBalance;

	if( amount < 0.0)
	{
          return false; // can not deposit a negative amount
	}

	else
	{
          newAccountBalance = accountBalance + amount;
          accountBalance = newAccountBalance;
	  return true;
         }

     }
 }
```

###Example of a race condition in Java

You've now seen the code above, but let's get into the problems that we can run into
when we have a multi-threaded application. The problem that we will be presenting below is what's called a
race condition. A race condition occurs when a program or application malfunctions because of an unexpected ordering of events that produces contention over the same resource. That sounds confusing, but it will make a lot more sense once you read the example below.

So, let’s get into the actual problem. Let’s say that there’s a husband and wife - Jack and Jill - who share a joint account. They currently have $1,000 in their account. They both log in to their online bank account at the same time, but from different locations.

They both decide to deposit $200 each into their account through a wire transfer from other bank accounts that they have at the same time. So, the total account balance after these 2 deposits should be $1,000 + ($200 * 2), which equals $1,400.

Let’s say Jill’s transaction goes through first, but Jill's thread of execution is switched out (to Jack’s transaction thread) right after executing this line of code in the deposit method:


newAccountBalance = accountBalance + amount;

Now, the processor is running the thread for Jack, who is also depositing $200 into their account. When Jack’s thread deposits $200, the account balance is still only $1,000, because the variable accountBalance has not yet been updated in Jill’s thread. Remember that Jill’s thread stopped execution right before the accountBalance variable was updated.

So, Jack’s thread runs until it completes the deposit function, and then updates the value of the accountBalance variable to $1200. After this, control returns to Jill’s thread, where newAccountBalance has the value of $1200. Then, it just assigns this value of $1,200 to accountBalance and returns. And that is the end of execution.

What is the result of these 2 deposits of $200? Well, the accountBalance variable ends up being set to only $1200, when it should have been $1400. This means Jack and Jill lost $200. This is good for the bank, but a huge problem for Jack and Jill, and any other of the bank's customers.

The cause of the race condition


So, do you see how the problem was caused here? Because Jill’s thread switched out (to Jack’s thread) right before the accountBalance variable was updated, Jill’s deposit was not counted.

If you remember the definition of a race condition, the example we just gave should clear it up. Here's the definition of a race condition again, in case you forgot: *A race condition occurs when a program or application malfunctions because of an unexpected ordering of events that produces contention over the same resource.* Hopefully, now it makes a lot more sense.

Synchronization fixes race conditions in multi-threaded programs

But the real question is how can this problem be fixed? Well, it should be clear that the code needs to allow the deposit function to run to completion without switching to run a different thread. This is what synchronization is all about - fixing issues like this! This can be accomplished with a synchronization construct like a monitor.

###Example of using the synchronized keyword in Java

This problem is easily fixed in Java. In the code below, all we do is add the synchronized keyword to the transfer and deposit methods to create a monitor. If you need a refresher on monitors then you can read this article: Monitors vs semaphores.

```java
public class BankAccount {

    int accountNumber;

    double accountBalance;


    // to withdraw funds from the account
    public synchronized boolean transfer (double amount)
    {
        double newAccountBalance;

        if( amount > accountBalance)
	{
             //there are not enough funds in the account
             return false;
	}

	else
	{
            newAccountBalance = accountBalance - amount;
            accountBalance = newAccountBalance;
            return true;
        }

    }

    public synchronized boolean deposit(double amount)
    {
	double newAccountBalance;

	if( amount < 0.0)
	{
          return false; // can not deposit a negative amount
	}

	else
	{
          newAccountBalance = accountBalance + amount;
          accountBalance = newAccountBalance;
	  return true;
         }

     }
 }
```

###Synchronized keyword locks methods

What does the synchronized keyword do for us here? Well, if a thread is executing inside either the deposit or transfer blocks, then it is now impossible for any other threads to enter either of those methods. This means that only one thread can execute those functions at a time - which is exactly what we want to prevent the problem with the accountBalance variable that we described earlier.

First, it is not possible for two invocations of synchronized methods on the same object to interleave - so one thread can not interrupt another thread until it is done executing all of the code in a synchronized method. So, when one thread is executing a synchronized method all other threads are blocked from entering that method.


##What is the difference between a System Thread and a User Thread?

There is a difference between user threads and system threads, and it helps to explain that difference. The system creates the system thread (no surprise there). Everything starts with the system thread – it is the first and main thread. The application usually ends when the system thread terminates. User threads are created by the application to do tasks that either cannot or should not be done by the system thread.

Applications which display user interfaces have to be careful when using threads. The system (or main) thread in these types of applications is also called the event thread – because it waits for and submits events (like clicks of the mouse and keyboard actions) to the application for processing. Allowing the event/system thread to be blocked for any period of time is generally considered bad programming practice, because it can lead to an unresponsive application or even a frozen computer. The problem of a blocked event thread is avoided by creating user threads to handle time consuming operations.

So, What are The Differences Between System and User Threads?


From the discussion above, you can probably extract this information, but we thought we would make it very clear. System threads are the main threads used in an application, whereas user threads are created to handle different tasks as they come to the application.
