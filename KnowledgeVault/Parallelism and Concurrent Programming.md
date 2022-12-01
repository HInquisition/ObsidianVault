# Parallelism and Concurrent Programming

[[Measuring Computing Performance]]

## Defining Concurrency and Parallelism 

[[Concurrency]]

[[Parallelism]]
- [[Implicit versus Explicit Parallelism]]
- [[Task versus Data Parallelism]]

[[Flynn’s Taxonomy]]
[[Orthogonality of Concurrency and Parallelism]]

## Implicit Parallelism

[[Implicit Parallelism]]

[[Pipelined CPU]]
- [[Latency versus Throughput]]
- [[Pipeline Depth]]
- [[Pipeline Stalls]]
- [[Data Dependencies]]
- [[Instruction Reordering]]
- [[Out-of-Order Execution]]
- [[Branch Dependencies]]
- [[Speculative Execution]] / [[Branch Prediction]]
- [[Predication]]

[[Superscalar CPU]]
- [[Complexity of Superscalar Designs]]
- [[Superscalar and RISC]]

[[VLIW]]

## Explicit Parallelism

[[Hyperthreading]]
[[Multicore CPUs]]
[[Symmetric versus Asymmetric Multiprocessing]]
[[Distributed Computing]]

## OS Fundaments

[[The Kernel]]
- [[Kernel Mode versus User Mode]]
- [[Kernel Mode Privileges]]
- [[Kernel Calls]]

[[Interrupts]]
[[Preemptive Multitasking]]

[[Processes]]
- [[Anatomy of a Process]]
- [[Virtual Memory Map of a Process]]

[[Threads]]
- [[Thread Libraries]]
- [[Thread Creation and Termination]]
- [[Joining Threads]]
- [[Polling, Blocking and Yielding]]
- [[Context Switching]]
- [[Thread Priorities and Affinity]]
- [[Thread Local Storage]]

[[Fibers]]
- [[Fiber Creation and Destruction]]
- [[Fiber States]]
- [[Fiber Migration]]
- [[Debugging with Fibers]]

[[User-Level Threads]]
- [[Coroutines]]
- [[Kernel Threads versus User Threads]]

## Introduction to Concurrent Programming

[[Why Write Concurrent Software]]
[[Concurrent Programming Models]]

[[Race Condition]]
- [[Critical Race]]
- [[Data Race]]

[[Critical Operations and Atomicity]]
- [[Invocation and Response]]
- [[Atomicity Defined]]
- [[Making an Operation Atomic]]
- [[Atomicity as Serialization]]
- [[Data-Centric Consistency Models]]

## Thread Synchronization Primitives

[[Thread Synchronization Primitives]]

[[Mutexes]]
[[Critical Sections]]
[[Condition Variables]]

[[Semaphores]]
- [[Mutex versus Binary Semaphore]]
- [[Implementing a Semaphore]]

[[Windows Events]]

## Problems with Lock-Based concurrency

[[Problems with Lock-Based Concurrency]]