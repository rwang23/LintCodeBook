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

Reading the previous discussion on virtual memory is recommended to better understand this problem. A page fault occurs when a program tries to access a page that is mapped in address space, but not loaded in the physical memory (the RAM). In other words, a page fault occurs when a program can not find a page that it’s looking for in the physical memory, which means that the program would have to access the paging file (which resides on the hard disk) to retrieve the desired page.

The term page fault is a bit misleading as it implies that something went seriously wrong. Although page faults are undesirable – as they result in slow accesses to the hard disk – they are quite common in any operating system that uses virtual memory.


Now, we need to actually solve the problem. The easiest way to do this is to break the problem down into 12 steps (where 12 is the number of pages) to see what happens each time a page is referenced by the program, and at each step see whether a page fault is generated or not. Of course, we want to keep track of what pages are currently in the physical memory (the RAM). The first four page accesses will result in page faults because the frames are initially empty. After that, if the program tries to access a page that’s already in one of the frames then there’s no problem. But if the page that the program is trying to access is not already in one of the frames then that results in a page fault. In this case, we have to determine which page we want to take out (or ‘swap’) from the RAM, and for that we use the LRU algorithm.

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
