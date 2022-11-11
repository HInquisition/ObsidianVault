# Pipelined CPU

In order for a single [[Machine Language|machine language]] instruction to be executed by the [[CPU]], it must pass through a number of distinct stages. Every CPU’s design is a bit different—some CPU designs employ a large number of granular stages, while others utilize a smaller number of coarse-grained stages. 

However every CPU implements the following basic stages in one way or another:

- Fetch. The instruction to be executed is read from the memory location pointed to by the [[Registers|instruction pointer register (IP)]].
- Decode. The instruction word is decomposed into its opcode, addressing mode and optional operands.
- Execute. Based on the opcode, the appropriate functional unit within the CPU is selected ([[ALU]], [[FPU|FPU]], [[Memory controller]], etc.). The instruction is dispatched to the selected component for processing, along with any relevant operand data. The functional unit then performs its operation.
- Memory access. If the instruction involves reading or writing memory, the memory controller performs the appropriate operation during this stage.
- Register write-back. The functional unit executing the instruction (ALU, FPU, etc.) writes its results back into the destination register.

![[Pasted image 20221111150802.png]]

This figure traces the path of two instructions named “A” and “B” through the five execution phases of a serial CPU. This diagram contains a lot of blank space: While one stage is busy doing its thing to an instruction, all the other stages are twiddling their thumbs, doing nothing.

Each of the stages of instruction execution is actually handled by different
hardware within the CPU. 

![[Pasted image 20221111151521.png]]

The [[CU, Control Unit]] and [[Memory controller]] handle the instruction fetch stage. A different circuit within the CU then handles the decode stage. The [[ALU]], [[FPU]] or [[Vector processing unit, VPU|VPU]] handles the lion’s share of the execute stage. The memory stage is performed by the memory controller. And finally, the write-back stage primarily involves the
[[Registers]]. This division of labor amongst different circuits within the CPU is the key to making the CPU more efficient: We just need to keep all the stages’ hardware busy all the time.

The solution is known as <mark style="background: #D2B3FFA6;">pipelining</mark>. Instead of waiting for each instruction to complete all five stages before starting to execute the next one, we begin the execution of a new instruction on every clock cycle. Multiple instructions are therefore “in flight” simultaneously.

![[Pasted image 20221111152350.png]]

Pipelining is a bit like doing laundry. If you have a large number of loads to do, it wouldn’t be very efficient to wait until each load has been washed and dried before starting the next one—while the washer is busy, the dryer would be sitting idle, and vice versa. It’s much better to keep both machines busy at all times, by starting the second load washing just as soon as the first load goes into the dryer, and so on.

Pipelining is a form of parallelism known as [[Implicit Parallelism|Instruction-level parallelism (ILP)]]. For the most part, ILP is designed to be transparent to the programmer. Ideally, at a given clock speed, a program that runs properly on a scalar CPU should be able to run correctly—but faster—on a pipelined CPU. In theory, a CPU with a pipeline that is N stages deep can execute a program N times faster than its serial counterpart. 

However, pipelining doesn’t always perform as well as we would expect, thanks to various kinds of dependencies between instructions in the instruction stream.  
[[Data Dependencies]] 
[[Branch Dependencies]]
[[Resource Dependencies).]]