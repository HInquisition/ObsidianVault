# Blocking [[Threads]]

If we expect our thread to wait for a relatively long period of time for a condition to become true, busy-waiting is not a good option. Ideally we’d like to put our thread to sleep so that it doesn’t waste CPU resources, and rely on [[The Kernel]] to wake it back up when the condition becomes true at some future time. This is called <mark style="background: #D2B3FFA6;">blocking</mark> the thread.

A thread blocks by making a special kind of operating system call known as a <mark style="background: #D2B3FFA6;">blocking function</mark>. If the condition is already true at the moment a blocking function is called, the function won’t actually block—it will simply return immediately.

But if the condition is false, the kernel will put the thread to sleep, and add the thread and the condition on which it is waiting into a table. Later, when the condition becomes true, the kernel uses this internal table to identify and wake up any threads that are waiting on that condition.

There are all sorts of OS functions that block. Here are a few examples:

- Opening a file. Most functions that open a file such as `fopen()` will block the calling thread until the file has actually been opened (which may take hundreds or even thousands of cycles). Some functions, like `open()` under Linux, offer a non-blocking option (O_NONBLOCK) to support asynchronous file I/O.

- Explicit sleeping. Some functions explicitly put the calling thread to sleep for a specified length of time. Variants include `usleep()` (Linux), `Sleep()` (Windows) `std::this_thread::sleep_until()` (C++11 standard library) and `pthread_sleep() `(POSIX threads).

- Joining with another thread. A function such as `pthread_join()` blocks the calling thread until the thread being waited on has terminated. 

- Waiting for a mutex lock. Functions like `pthread_mutex_wait()` attempt to obtain an exclusive lock on a resource via an operating system object known as a [[Mutexes|mutex]]. If no other thread holds the lock, the function grants the lock to the calling thread and returns immediately; otherwise, the calling thread is put to sleep until the lock can be obtained.

Operating system calls aren’t the only functions that can block. Any users-pace function that ultimately calls a blocking OS function is itself considered to be a blocking function. It’s a good idea to document such a function, so that the programmers who use it will know that it has the potential to block.