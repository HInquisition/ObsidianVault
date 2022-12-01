# Fibers

In [[Preemptive Multitasking]], [[Threads|thread]] scheduling is handled automatically by [[The Kernel]]. This is often convenient, but sometimes programmers find it desirable to have control over the scheduling of workloads in their programs. For example, when implementing a job system for a game engine (see [[Job System]]), we might want to allow jobs to explicitly [[Yielding Threads|yield]] the CPU to other jobs, without worrying about the possibility of preemption “pulling the rug out” from under our jobs as they run. In other words, sometimes we want to use [[Cooperative Multitasking|cooperative]] rather than [[Preemptive Multitasking|preemptive]] multitasking.

Some operating systems provide just such a cooperative multitasking mechanism: They are known as <mark style="background: #D2B3FFA6;">fibers</mark>. A fiber is a lot like a thread, in that it represents a running instance of a stream of [[Machine Language|machine language]] instructions. A fiber has a [[Call Stack|call stack]] and register state (an [[Context Switching|execution context]]), just like a thread. However, the big difference is that a fiber is never scheduled directly by the kernel. Instead, fibers run within the context of a thread, and are scheduled cooperatively, by each other.

More about fibers:
- [[Fiber Creation and Destruction]]
- [[Fiber States]]
- [[Fiber Migration]]
- [[Debugging with Fibers]]