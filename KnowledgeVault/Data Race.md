# Data Races

A <mark style="background: #D2B3FFA6;">data race</mark> is a [[Critical Race|critical race condition]] in which two or more flows of control interfere with one another while reading and/or writing a block of shared data, resulting in data corruption. Data races are <mark style="background: #FF5582A6;">the central problem</mark> of concurrent programming. Writing concurrent programs always boils down to eliminating data races, either by carefully controlling access to shared data, or by replacing shared data with private, independent copies of data (thereby transforming a concurrency problem into a sequential programming problem). 

To better understand data races, consider the following simple snippet of C/C++ code:
```C++
int g_count = 0;
inline void IncrementCount()
{
++g_count;
}
```
If you compiled this code for an Intel x86 CPU and viewed the disassembly, it would look something like this:
```
mov eax,[g_count] ; read g_count into register EAX
inc eax           ; increment the value
mov [g_count],eax ; write EAX back into g_count
```
This is an example of a *read-modify-write* (RMW) operation.

Now imagine that two threads A and B were both to call the Increment `Count()` function concurrently (either in parallel or via preemptive multithreading). Under normal operation, if each thread called the function exactly once, we’d expect the final value of `g_count` to be 2, because either thread A increments `g_count` and then thread B increments it, or vice-versa.

![[Pasted image 20221201171034.png]]
*Example of correct operation of a simple two-threaded concurrent program. First thread A reads the contents of a shared variable, increments the value, and writes the results back into the shared variable. At a later time, thread B does the same steps. The final value of the shared variable is 2 as expected*

Next let’s consider the case of our two threads running on a single-core machine with [[Preemptive Multitasking]]. Let’s say that thread A runs first, and has just finished executing the first `mov` instruction when a [[Context Switching|context switch]] to thread B occurs. Instead of thread A executing its `inc` instruction, thread B runs its first `mov` instruction. After some time thread B’s quantum expires, and the kernel context switches back to thread A, which continues where it left off and executes the `inc` instruction. Hint: It’s not good! The final value of `g_count` is no longer 2 as it should be.

![[Pasted image 20221201171432.png]]
*Example of a [[Race Condition|race condition]]. Thread A reads the value of the shared variable, but then is preempted by thread B, which also reads the (same) value. By the time both threads have incremented the value and written their results back to the shared variable, the global variable contains the incorrect value 1 instead of the expected value of 2.*

If we run our two threads on parallel hardware, a similar bug can occur, although for a slightly different reason. As in the single-core case, we might get lucky: The two read-modify-write operations might not overlap at all, and the result will be correct. However, if the two read-modify-write operations overlap, either offset from one another or in perfect synchronization, both threads can end up loading the same value of `g_count` into their respective `EAX` registers. Both will increment the value, and both will write it to memory. One thread will overwrite the results of the other, but it doesn’t really matter— because they both loaded the same initial value, the final value of `g_count` will end up being incorrect, just as it was in the single-core scenario. The three data race scenarios (preemption, offset overlap, and perfect synchronization) are illustrated in this Figure:

![[Pasted image 20221201171900.png]]