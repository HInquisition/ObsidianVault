# [[Memory]] Architecture

In a simple von Neumann [[Computer architecture]], memory is treated as a single
homogeneous block, all of which is equally accessible to the [[CPU]]. In reality,
a computer’s memory is almost never architected in such a simplistic manner.
For one thing, the CPU’s [[Registers]] are a form of memory, but registers
are typically referenced by name in an assembly language program, rather
than being addressed like ordinary [[ROM]] or [[RAM]]. Moreover, even “regular”
memory is typically segregated into blocks with different characteristics and
different purposes. This segregation is done for a variety of reasons, including
cost management and optimization of overall system performance.

## Memory Mapping

An n-bit [[Address Bus]] gives the [[CPU]] access to a theoretical address space that is $2^n$ bytes in size. An individual memory device ([[ROM]] or [[RAM]]) is always
addressed as a contiguous block of memory cells. So a computer’s address
space is typically divided into various contiguous segments. One or more of
these segments correspond to [[ROM]] memory modules, and others correspond
to [[RAM]] modules.

For example on the Apple II, the 16-bit addresses in the
range `0xC100` through `0xFFFF` were assigned to [[ROM]] chips (containing the
computer’s [[Firmware]]), while the addresses from `0x0000` through `0xBFFF` were
assigned to [[RAM]]. Whenever a physical memory device is assigned to a range
of addresses in a computer’s address space, we say that the address range has
been mapped to the memory device.

Of course a computer may not have as much memory installed as could
be theoretically addressed by its [[Address Bus]]. A 64-bit address bus can access
16 EiB of memory, so we’d be unlikely to ever fully populate such an
address space! Therefore, it’s common place for some segments of a computer’s address space to remain unassigned.

## Memory-Mapped I/O

Address ranges needn’t all map to memory devices—an address range might
also be mapped to other peripheral devices, such as a joypad or a network interface card (NIC). This approach is called memory-mapped I/O because the [[CPU]]
can perform I/O operations on a peripheral device by reading or writing to addresses, just as if they were ordinary [[RAM]]. Under the hood, special circuitry
detects that the [[CPU]] is reading from or writing to a range of addresses that
have been mapped to a non-memory device, and converts the read or write
request into an I/O operation directed at the device in question.

As a concrete example, the Apple II mapped I/O devices into the address range `0xC000` through `0xC0FF`, allowing programs to do things like control bank-switched
[[RAM]], read and control voltages on the pins of a game controller socket on the
motherboard, and perform other I/O operations by merely reading from and
writing to the addresses in this range.

Alternatively, a [[CPU]] might communicate with non-memory devices via special [[Registers]] known as [[Ports]]. In this case, whenever the [[CPU]] requests that data be read from or written to a port register, the hardware converts the request into an I/O operation on the target device. This approach is called portmapped I/O. In the Arduino line of microcontrollers, port-mapped I/O gives a program direct control over the digital inputs and outputs at some of the pins of the chip.

## [[VRAM]]
Raster-based display devices typically read a hard-wired range of physical
memory addresses in order to determine the brightness/color of each pixel on
the screen. A range of memory addresses assigned for use by a video controller is known as video [[RAM]] ([[VRAM]]). 
## Case Study: The Apple II Memory Map
To illustrate the concepts of memory mapping, let’s look at a simple real-world
example. The Apple II had a 16-bit address bus, meaning that its address
space was only 64 KiB in size. This address space was mapped to [[ROM]], [[RAM]],
memory-mapped I/O devices and [[VRAM]] regions as follows:

```
0xC100 - 0xFFFF ROM (Firmware)
0xC000 - 0xC0FF Memory-Mapped I/O
0x6000 - 0xBFFF General-purpose RAM
0x4000 - 0x5FFF High-res video RAM (page 2)
0x2000 - 0x3FFF High-res video RAM (page 1)
0x0C00 - 0x1FFF General-purpose RAM
0x0800 - 0x0BFF Text/lo-res video RAM (page 2)
0x0400 - 0x07FF Text/lo-res video RAM (page 1)
0x0200 - 0x03FF General-purpose and reserved RAM
0x0100 - 0x01FF Program stack
0x0000 - 0x00FF Zero page (mostly reserved for DOS)
```

We should note that the addresses in the Apple II memory map corresponded
directly to memory chips on the motherboard. In today’s operating systems,
programs work in terms of virtual addresses rather than physical addresses.

## [[Virtual Memory]] Mapping
Most modern CPUs and operating systems support a memory remapping feature
known as a virtual memory system. In these systems, the memory addresses
used by a program don’t map directly to the memory modules installed in the
computer. Instead, whenever a program reads from or writes to an address,
that address is first remapped by the CPU via a look-up table that’s maintained
by the OS.