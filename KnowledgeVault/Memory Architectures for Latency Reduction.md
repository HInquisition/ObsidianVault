# [[Memory Architecture|Memory Architectures]] for Latency Reduction

The speed with which data can be accessed from a memory device is an important characteristic. We often speak of memory access latency, which is defined as
the length of time between the moment the [[CPU]] requests data from the memory system and the moment that that data is actually received by the [[CPU]]. 

Memory access latency is primarily dependent on three factors:
1. The technology used to implement the individual memory cells,
2. The number of read and/or write ports supported by the memory
3. The physical distance between those memory cells and the [[CPU]] core that uses them.

The access latency of _static_ RAM ([[SRAM]]) is generally much lower than that of
_dynamic_ RAM ([[DRAM]]). [[SRAM]] achieves its lower latency by utilizing a more complex design which requires more [[Transistor|transistors]] per bit of memory than does [[DRAM]]. This in turn makes [[SRAM]] more expensive than [[DRAM]], both in terms of financial cost per bit, and in terms of the amount of real estate per bit that it consumes on the die.

The simplest memory cell has a single port, meaning only one read or write
operation can be performed by it at any given time. Multi-ported [[RAM]] allows
multiple read and/or write operations to be performed simultaneously,
thereby reducing the latency caused by contention when multiple cores, or
multiple components within a single core, attempt to access a bank of memory
simultaneously. As you’d expect, a multi-ported RAM requires more transistors
per bit than a single-ported design, and hence it costs more and uses more
real estate on the die than a single-ported memory.

The physical distance between the [[CPU]] and a bank of [[RAM]] also plays a role in determining the access latency of that memory. This is because electronic signals travel at a finite speed within the computer. In theory, electronic signals are comprised of electromagnetic waves, and hence travel at close to the speed of light. Additional latencies are introduced by the various switching and logic circuits that a memory access signal encounters on its journey through the system. As such, the closer a memory cell is to the CPU core that uses it, the lower its access latency tends to be.

![[The Memory Gap]]

## Solving The Memory Gap Problem

Programmers and hardware designers have together developed a wide range of techniques to work around the problems caused by high memory access latency. These techniques usually focus on one or more of the following:
1. Reducing average memory latency by placing smaller, faster memory banks closer to the CPU core, so that frequently-used data can be accessed more quickly;
2. “Hiding” memory access latency by arranging for the CPU to do other useful work while waiting for a memory operation to complete; 
3. Minimizing accesses to main memory by arranging a program’s data in as efficient a manner as possible with respect to the work that needs to be done with that data.

## Latency reduction techniques

![[Register Files#Registers Register Files]]