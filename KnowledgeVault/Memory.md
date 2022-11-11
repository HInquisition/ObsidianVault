# Memory

The memory in a computer acts like a bank of mailboxes at the post office, with
each box or “cell” typically containing a single byte of data (an eight-bit value).
Each one-byte memory cell is identified by its address—a simple scheme ranging from 0 to $N - 1$, where $N$ is the size of addressable memory in bytes.

[[Memory Architecture]]
[[Memory Architectures for Latency Reduction]]
[[Memory Cache]]
[[Virtual Memory]]
[[Memory Alignment]]

Memory comes in two basic flavors:
• read-only memory ([[ROM]])
• read/write memory, known for historical reasons as random access memory
([[RAM]]).

[[ROM]] modules retain their data even when power is not applied to them.
Also they not really designed to be reprogrammed in most cases.

[[RAM]] can be further divided into static RAM ([[SRAM]]) and dynamic RAM
([[DRAM]]). Both static and dynamic RAM retain their data as long as power
is applied to them. 

RAM can also be categorized by various other design characteristics, such
as:
• whether it is **multi-ported**, meaning that it be accessed simultaneously by
more than one component within the [[CPU]];
• whether it operates by being synchronized to a clock ([[SDRAM]]) or asynchronously;
• and whether or not it supports **double data rate access** ([[DDR]]), meaning
the RAM can be read or written on both rising and falling [[Clock]]

