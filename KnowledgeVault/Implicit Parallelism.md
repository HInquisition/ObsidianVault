# Implicit [[Parallelism]]

Implicit parallelism refers to the use of parallel hardware components within a CPU for the purpose of improving the performance of a single instruction stream. This is also known as <mark style="background: #D2B3FFA6;">instruction level parallelism (ILP)</mark>, because the [[CPU]] executes instructions from a single stream (a single thread) but each instruction is executed with some degree of hardware parallelism. 

Examples of implicit parallelism include:
- [[Pipelined CPU|pipelining]],
- [[Superscalar CPU|superscalar architectures]], 
- [[VLIW|very long instruction word (VLIW) architectures]].

[[GPU]]s also make extensive use of implicit parallelism

CPU manufacturers began using implicit parallelism in their consumer products in the late 1980s, in an attempt to make **existing code** run faster on each new generation of CPUs within a given product line.