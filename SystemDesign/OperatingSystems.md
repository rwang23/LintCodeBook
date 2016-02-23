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

It’s important to note that a thread can do anything a process can do. But since a process can consist of multiple threads, a thread could be considered a ‘lightweight’ process. Thus, the essential difference between a thread and a process is the work that each one is used to accomplish. Threads are used for small tasks, whereas processes are used for more ‘heavyweight’ tasks – basically the execution of applications.

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
