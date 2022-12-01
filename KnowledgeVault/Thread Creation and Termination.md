# Thread Creation and Termination

When an executable file is run, the [[Processes|process]] created by the OS to encapsulate it automatically contains a single [[Threads|thread]], and execution of this thread begins at the entry point of the program—in C/C++ this is the special function `main()`. This “main thread” can spawn new threads if desired, by making calls to an operating system specific function such as `pthread_create()` (POSIX threads), `CreateThread()` (Windows), or by instantiating an instance of a thread class such as `std::thread` (C++11). The new thread begins execution at an entry point function whose address is provided by the caller. Once created, a thread will continue to exist until it terminates. 

The execution of a thread can terminate in a number of ways:

- It can end “naturally” by *returning* from its entry point function. (In the special case of the main thread, returning from main() not only ends the thread, but also ends the entire process.)
- It can call a function such as `pthread_exit()` to *explicitly terminate* its execution before having returned from its entry point function.
- It can be *killed* externally by another thread. In this case, the external thread makes a *request* to cancel the thread in question, but the thread may not respond immediately to the request, or it may ignore the request entirely. The cancelability of a thread is determined when that thread is created.
- It can be forcibly killed because its process has ended. (A process terminates when the main thread returns from the `main()` entry point function, when any thread calls `exit()` to kill the process explicitly, or when an external actor kills the process.)