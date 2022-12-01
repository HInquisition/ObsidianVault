# Preemptive Multitasking

The earliest minicomputers and personal computers ran a single program at a time. They were inherently serial computers, capable of reading a program from a single instruction stream, and executing one instruction from this stream at a time. The disk operating systems (DOS) in those days weren’t much more than glorified device drivers, allowing programs to interface with devices such as tape, floppy and hard disk drives. The entire computer would be devoted to running a single program at a time. 

![[Cooperative Multitasking#Cooperative multitasking]]

In preemptive multitasking, programs still share the CPU by time-slicing. However the scheduling of programs is controlled by the operating system, not via cooperation between the programs themselves. As a result, each program gets a regular, consistent and reliable time slice on the CPU. The time slice during which one particular program is allowed to run on the CPU is sometimes called the program’s quantum. To implement preemptive multitasking, the operating system responds to a regularly-timed hardware interrupt in order to periodically context switch between the different programs running on the system. 
(See [[Context Switching]])

We should note here that preemptive multitasking is used even on multicore machines, because typically the number of threads is greater than the number of cores. For example, if we were to have 100 threads and only four CPU cores, then the kernel would use preemptive multitasking to time-slice between 25 threads on each core.