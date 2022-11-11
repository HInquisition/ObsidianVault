# Virtual [[Memory Architecture|Memory]]

Most modern [[CPU]] and operating systems support a memory remapping feature
known as a virtual memory system. In these systems, the memory addresses
used by a program don’t map directly to the memory modules installed in the
computer. Instead, whenever a program reads from or writes to an address,
that address is first remapped by the [[CPU]] via a look-up table that’s maintained
by the [[OS]]. The remapped address might end up referring to an actual cell in
memory (with a totally different numerical address). It might also end up referring
to a block of data on-disk. Or it might turn out not to be mapped to
any physical storage at all. In a virtual memory system, the addresses used
by programs are called virtual addresses, and the bit patterns that are actually
transmitted over the [[Address Bus]] by the memory controller in order to access
a [[RAM]] or [[ROM]] module are called physical addresses.

Virtual memory is a powerful concept. It allows programs to make use
of more memory than is actually installed in the computer, because data can
overflow from physical [[RAM]] onto disk. Virtual memory also improves the
stability and security of the operating system, because each program has its
own private “view” of memory and is prevented from stomping on memory
blocks that are owned by other programs or the operating system itself. 

## Virtual Memory Pages

To understand how this remapping takes place, we need to imagine that the
entire addressable memory space (that’s $2^n$ byte-sized cells if the [[Address Bus]]
is n bits wide) is conceptually divided into equally-sized contiguous chunks
known as pages. Page sizes differ from [[OS]] to OS, but are always a power of
two—a typical page size is 4 KiB or 8 KiB. Assuming a 4 KiB page size, a 32-bit
address space would be divided up into 1,048,576 distinct pages, numbered
from `0x0` to `0xFFFFF`

![[Pasted image 20221018222525.png]]

## Virtual to Physical Address Translation

Whenever the [[CPU]] detects a memory read or write operation, the address is
split into two parts: the **page index** and an **offset** within that page (measured in
bytes). For a page size of 4 KiB, the offset is just the lower 12 bits of the address,
and the page index is the upper 20 bits, masked off and shifted to the right by
12 bits. For example, the virtual address `0x1A7C6310` corresponds to an offset
of `0x310` and a page index of `0x1A7C6`.

The page index is then looked up by the CPU’s memory management unit
([[MMU]]) in a page table that maps virtual page indices to physical ones. (The
page table is stored in [[RAM]] and is managed by the operating system.) If the
page in question happens to be mapped to a physical memory page, the virtual
page index is translated into the corresponding physical page index, the bits
of this physical page index are shifted to the left as appropriate and OR-ed
together with the bits of the original page offset, and voila! We have a physical
address. So to continue our example, if virtual page `0x1A7C6` happens to map
to physical page `0x73BB9`, then the translated physical address would end up
being `0x73BB9310`. This is the address that would actually be transmitted over
the [[Address Bus]].

![[Pasted image 20221025182602.png]]
## The Translation Lookaside Buffer (TLB)

Because page sizes tend to be small relative to the total size of addressable memory (typically 4 KiB or 8 KiB), the page table can become very large. Looking up physical addresses in the page table would be time-consuming if the entire table had to be scanned for every memory access a program makes. To speed up access, a caching mechanism is used, based on the assumption that an average program will tend to reuse addresses within a relatively small number of pages, rather than read and write randomly across the entire address range. A small table known as the translation lookaside buffer (TLB) is maintained within the [[MMU]] on the [[CPU]] die, in which the virtual-to-physical address mappings of the most recently-used addresses are cached. Because this buffer is located in close proximity to the [[MMU]], accessing it is very fast. The TLB acts a lot like a general purpose memory cache hierarchy (see [[Memory Cache]]), except that it is only used for caching page table entries. 


