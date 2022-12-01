# Concurrency

A concurrent piece of software utilizes multiple **flows of control** to solve a problem. These flows of control might be implemented as multiple **[[Threads]]** running within the context of a single [[Processes|process]], or multiple cooperating processes running either on a single computer or multiple computers. Multiple flows of control can also be implemented within a process using other techniques such as [[Fibers]] or [[Coroutines]].

The primary factor that distinguishes concurrent programming from sequential programming is the **reading and/or writing of shared data**. If we have two or more flows of control, each operating on a totally independent block of data, then this is not technically an example of concurrency—it’s just “computing at the same time.”

![[Pasted image 20221106175856.png]]

The central problem of concurrent programming is how to coordinate multiple readers and/or multiple writers of a shared data file, in such a way as to ensure predictable, correct results. At the heart of this problem is a special kind of [[Race Condition]] known as a [[Data Race]], in which two or more flows of control “compete” to be the first to read, modify and write a chunk of shared data. The crux of the concurrency problem is to identify and eliminate data races.
