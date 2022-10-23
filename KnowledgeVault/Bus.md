# Bus, Шина 
Data is transferred between the [[CPU]] and [[Memory]] over connections known
as **buses**. A bus is just a bundle of parallel digital “wires” called **lines**, each
of which can represent a single bit of data. 

When the line carries a voltage signal it represents a binary one, and when the line has no voltage (0 volts) it represents a binary zero. 
A bundle of $n$ single-bit lines arranged in parallel can transmit an $n$-bit number (i.e., any number in the range $0$ through $2n-1$)

Buses use less area on a circuit board and need less power than a huge number of direct connections. It can also need fewer pins on the chip or chips that includes the CPU

## Buses:
 - **[[System bus]]**


## Bus Widths
The width of the address bus, measured in bits, controls the range of possible
addresses that can be accessed by the [[CPU]] (i.e., the size of addressable memory in the machine). 

For example, a computer with a 16-bit address bus can access at
most 64 KiB of memory, using addresses in the range `0x0000` through `0xFFFF`. A
computer with a 32-bit address bus can access a 4 GiB memory, using addresses
in the range `0x00000000` through `0xFFFFFFFF`. And a machine with a 64-bit
address bus can access a staggering $2^{64} = 16$  EiB (exbibytes) of memory. 

The width of the data bus determines how much data can be transferred
between [[CPU]] registers and [[Memory]] at a time. (The data bus is typically the
same width as the general-purpose registers in the CPU, although this isn’t
always the case.) An 8-bit data bus means that data can be transferred one
byte at a time—loading a 16-bit value from memory would require two separate
memory cycles, one to fetch the least-significant byte and one to fetch
the most-significant byte. At the other end of the spectrum, a 64-bit data bus
can transfer data between memory and a 64-bit register as a single memory
operation.

It’s possible to access data items that are narrower than the width of a machine’s
data bus, but it’s typically more costly than accessing items whose
widths match that of the data bus. For example, when reading a 16-bit value
on a 64-bit machine, a full 64 bits worth of data must still be read from memory.
The desired 16-bit field then has to be masked off and possibly shifted into
place within the destination register.
See [[Размерность и переносимость типа Int в C++]]