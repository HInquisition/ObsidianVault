# Threads

A thread encapsulates a running instance of a single stream of machine language instructions. Each thread within a [[Processes|process]] is comprised of:

- a *thread id* (TID) which is unique within its process, but may or may not be unique across the entire operating system;
- the thread’s *call stack*—a contiguous block of memory containing the stack frames of all currently-executing functions;
- the values of all special- and general-purpose [[Registers|registers]] including the instruction pointer (IP), which points at the current instruction in the thread’s instruction stream, the base pointer (BP) and stack pointer (SP) which define the current function’s stack frame;
- a block of general-purpose memory associated with each thread, known as *thread local storage* (TLS).

By default, a process contains a single main thread and hence executes a single instruction stream. This thread begins executing at the entry point of the program—typically the  `main()` function. However, all modern operating systems are capable of executing more than one concurrent instruction stream within the context of a single process. You can think of a thread as *the fundamental unit of execution* within the operating system. A thread provides the minimum resources required to execute an instruction stream—a [[Call Stack|call stack]] and a set of registers. The process merely provides the environment in which one or more threads execute. 

![[Pasted image 20221129181234.png]]
*A process encapsulates the resources required to run one or more threads. Each thread encapsulates an execution context comprised of the contents of the CPU’s registers and a call stack.*


![[Thread Libraries]]