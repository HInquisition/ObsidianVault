# User-Level Threads

Both [[Threads]] and [[Fibers]] tend to be rather “heavy weight” because these facilities are provided by [[The Kernel]]. This implies that most functions that you’d call to manipulate threads or fibers involve a context switch into kernel space—not a cheap operation. But there are lighter-weight alternatives to threads and fibers. These mechanisms allow programmers to code in terms of multiple independent flows of control, each with its own execution context, but without the high cost of making [[Kernel Calls]]. Collectively, these facilities are known as <mark style="background: #D2B3FFA6;">user-level threads</mark>.

User-level threads are implemented entirely in user space. The kernel knows nothing about them. Each user-level thread is represented by an ordinary data structure that keeps track of the thread’s id, possibly a human-readable name, and execution context information (the contents of CPU registers and a call stack). A user-level thread library provides API functions for creating and destroying threads, and context switching between them. Each user-level thread runs within the context of a “real” thread or fiber that has been provided by the operating system.
 
The trick to implementing a user-level thread library is figuring out how to implement a [[Context Switching|context switch]]. If you think about it, a context switch mostly boils down to swapping the contents of the CPU’s registers. After all, the registers contain all of the information needed to describe a thread’s execution context— including the instruction pointer and the call stack. So by writing some clever assembly language code, it’s possible to implement a context switch. And once you have a context switch, the rest of your user-level thread library is nothing more than data management.

User-level threads aren’t supported very well in C and C++, but some portable and non-portable solutions do exist. POSIX provided a collection of functions for managing lightweight thread execution contexts via its `ucontext.h` header file (https://en.wikipedia.org/wiki/Setcontext), but this API has since been deprecated. The C++ Boost library provides a portable user-level thread library. (Search for “context” on http://www.boost.org/ for documentation on this library.)

Also see [[Coroutines]] as an example of user-level threads. 