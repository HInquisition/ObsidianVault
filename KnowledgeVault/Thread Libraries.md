# Thread Libraries

All operating systems that support multithreading provide a collection of system calls for creating and manipulating [[Threads|threads]]. A few portable thread libraries are also available, the best known of which are the IEEE POSIX 1003.1c standard thread library (`pthread`) and the C11 and C++11 standard thread libraries. The Sony PlayStation 4 SDK provides a set of thread functions prefixed with `sce` that map pretty much directly to the POSIX thread API. The various thread APIs differ in their details, but all of them support the following basic operations:

1. *[[Thread Creation and Termination|Create]]*.   A function or class constructor that spawns a new thread. 
2. *[[Thread Creation and Termination|Terminate]].*  A function that terminates the calling thread.
3. *Request to exit.*  A function that allows one thread to request another thread to exit.
4. *Sleep.*  A function that puts the current thread to sleep for a specified length of time.
5. *[[Yielding Threads|Yield]].*  A function that yields the remainder of the thread’s time slice so other threads can get a chance to run.
6. *[[Joining Threads|Join]].*   A function that puts the calling thread to sleep until another thread or group of threads has terminated.