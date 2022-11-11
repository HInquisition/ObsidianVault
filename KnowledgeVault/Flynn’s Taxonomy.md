# Flynn’s Taxonomy

Yet another way to classify the varying degrees of [[Parallelism]] we’ll encounter in computing hardware is to use Flynn’s Taxonomy. Proposed by Michael J. Flynn of Stanford University in 1966, this approach breaks down parallelism into a two-dimensional space. Along one axis, we have the number of parallel flows of control (which Flynn refers to as the number of instructions running in parallel at any given moment). On the other axis, we have the number of distinct data streams being operated on by each instruction in the program.

![[Pasted image 20221106195053.png]]
The space is thus divided into four quadrants:
- Single instruction, single data (SISD): A single instruction stream operating on a single data stream.
- Multiple instruction, multiple data (MIMD): Multiple instruction streams operating on multiple independent data streams.
- [[Single instruction multiple data, SIMD|Single instruction, multiple data (SIMD)]]: A single instruction stream operating on multiple data streams (i.e., performing the same sequence of operations on multiple independent streams of data simultaneously).
- Multiple instruction, single data (MISD): Multiple instruction streams all operating on a single data stream. (MISD is rarely used in games, but one common application is to provide fault tolerance via redundancy.)

## Single versus Multiple Data

It’s important to realize here that a “data stream” isn’t just an array of numbers. Most arithmetic operators are binary—they operate on two inputs to produce a single output. When applied to binary arithmetic, the term “single data” refers to a single pair of inputs, with a single output. 

As an example, let’s have a look at how two binary arithmetic operations, a multiply ($a\times b$) and a divide ($c/d$ ), might be accomplished under each of the four Flynn categories:

- In a SISD architecture, a single ALU performs the multiply first, followed by the divide. 
![[Pasted image 20221106201534.png]]
- In a MIMD architecture, two ALUs perform operations in parallel, operating on two independent instruction streams.
![[Pasted image 20221106201740.png]]
- The MIMD classification also applies to the case in which a single ALU processes two independent instruction streams via **time-slicing**
![[Pasted image 20221106202023.png]]
- In a SIMD architecture, a single “wide ALU” known as a vector processing unit (VPU) performs the multiply first, followed by the divide, but each instruction operates on a pair of four-element input vectors and produces a four-element output vector. 
![[Pasted image 20221106202201.png]]
- In a MISD architecture, two [[ALU]]s process the same instruction stream (multiply first, followed by divide) and ideally produce identical results. This architecture is primarily useful for implementing fault tolerance via redundancy. ALU 1 acts as a “hot spare” for ALU 0 and vice-versa, meaning that if one of the ALUs experiences a failure, the system can seamlessly switch to the other.
![[Pasted image 20221106202538.png]]

## [[GPU]] Parallelism: SIMT

In recent years, a fifth classification has been added to Flynn’s taxonomy to account for the design of graphics processing units ([[GPU]]). [[Single instruction multiple thread (SIMT)|Single instruction multiple thread (SIMT)]] is essentially a hybrid between SIMD and MIMD, used primarily in the design of GPUs. It mixes SIMD processing (a single instruction operating on multiple data streams simultaneously) with multithreading (more than one instruction stream sharing a processor via time-slicing).

The term “SIMT” was coined by NVIDIA, but it can be used to describe the design of any GPU. The term <mark style="background: #D2B3FFA6;">manycore</mark> is also often used to refer to a SIMT design (i.e., a GPU consisting of a relatively large number of lightweight SIMD cores) whereas the term <mark style="background: #D2B3FFA6;">multicore</mark> refers to MIMD designs (i.e., a CPU with a relatively smaller number of heavyweight general purpose cores). 