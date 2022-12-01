# Superscalar CPUs

The [[Pipelined CPU]] is what is called a *scalar* processor. This means that it can start executing at most one instruction per clock cycle. Yes, multiple instructions are “in flight” at any given moment, but only one new instruction is sent down the pipeline every clock cycle. At its core, [[Parallelism]] is about making use of multiple hardware components simultaneously. So one way to double the throughput of a CPU (at least in theory!) would be to duplicate most of the components on the chip, in such a way that two instructions could be launched each clock cycle. This is called a <mark style="background: #D2B3FFA6;">superscalar architecture</mark>.

In a superscalar CPU, two (or more) instances of the circuitry that manages each stage of the pipeline1 is present on-chip. The CPU still fetches instructions from a single instruction stream, but instead of issuing the one instruction pointed to by the IP during each clock cycle, the next two instructions are fetched and dispatched during each clock cycle. 

![[Pasted image 20221122150734.png]]
A pipelined superscalar CPU contains multiple execution components (ALUs, FPUs and/or VPUs) fed by a single instruction scheduler which typically supports [[Out-of-Order Execution]] and [[Branch Prediction]]


![[Pasted image 20221122150804.png]]
Best-case execution of 14 instructions “A” through “N” on a superscalar pipelined CPU over seven clock cycles

![[Complexity of Superscalar Designs#Complexity of Superscalar designs]]