# Anatomy of a Process

Under the hood, a process consists of:
- a *process id* (PID) that uniquely identifies the process within the operating system;
- a set of *permissions*, such as which user “owns” each process and to which user group it belongs;
- a reference to the process’s *parent process*, if any,
- a *virtual memory space* containing the process’s “view” of physical memory (see [[Virtual Memory Map of a Process]] for more information);
- the values of all defined *environment variables*;
- the set of all open *file handles* in use by the process;
- the current *working directory* for the process,
- resources for managing *synchronization* and *communication* between processes in the system, such as message queues, pipes, and semaphores;
- one or more [[Threads|threads]].

A thread encapsulates a running instance of a single stream of [[Machine Language|machine language]] instructions. By default, a process contains a single thread. But more than one thread can be created within a process, allowing more than one instruction stream to run concurrently. [[The Kernel]] schedules all of the threads in the system (from all currently-running processes) to run on the available cores. It uses [[Preemptive Multitasking|preemptive multitasking]] to time-slice between threads when there are more threads than there are cores.

We should stress here that threads are *the fundamental unit of program execution* within an operating system, not processes. A process merely provides an environment within which its thread(s) can run, including a virtual memory map and a set of resources that are used by and shared between all threads within that process. Whenever a thread is scheduled to run on a core, its process becomes active, and that process’s resources and environment become available for use by the thread while it runs. So when we say that a thread is running on a core, remember that it is always doing so within the context of exactly one process.