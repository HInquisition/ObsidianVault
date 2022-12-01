# Virtual Memory Map of a Process

You’ll recall from [[Virtual Memory]] that a program generally never works directly with physical memory addresses. Rather, the program accesses memory in terms of virtual addresses, and the CPU and operating system cooperate to remap these virtual addresses into physical addresses. We said that the remapping of virtual to physical addresses happens in terms of contiguous blocks of addresses called pages, and that a page table is used by the OS to map virtual page indices to physical page indices.

Every process has its own virtual page table. This means that every process has its own custom view of memory. This is one of the primary ways in which the operating system provides a secure and stable execution environment. Two processes cannot corrupt each other’s memory, because the physical pages owned by one process are simply not mapped into the other process’s address space (unless they explicitly share pages). Also, pages owned by [[The Kernel]] are protected from inadvertent or deliberate corruption by a user process because they are mapped to a special range of addresses known as <mark style="background: #D2B3FFA6;">kernel space</mark> which can only be accessed by code running in [[Kernel Mode versus User Mode|kernel mode]].

A process’s virtual page table effectively defines its memory map. The memory map typically contains:

- the text, data and BSS sections as read in from the program’s executable file (see [[Структура исполняемого файла C++]]);
- a view of any shared libraries (DLLs, PRXs) used by the program;
- a call stack for each thread;
- a region of memory called [[Memory Heap (Куча)|the heap]] for dynamic memory allocation;
- possibly some pages of memory that are shared with other processes; and
- a range of kernel space addresses which are inaccessible to the process (but become accessible whenever a kernel call executes).

## Text, Data and BSS Sections

When a program is first run, the kernel creates a process internally and assigns it a unique PID. It then sets up a virtual page map for the process—in other words, it creates the virtual address space of the process. It then allocates physical pages as necessary and maps them into the virtual address space by adding entries to the process’s page table.

The kernel reads the executable file (text, data and BSS sections) into memory by allocating virtual pages and loading the data into them. This allows the program’s code and global data to be “visible” within the process’s virtual address space. The machine code in an executable file is actually relocatable, meaning that its addresses are specified as relative offsets rather than absolute memory addresses. These relative addresses are fixed up by the operating system, meaning they are converted back into real (virtual) addresses, prior to running the program. (For more on the format of an executable file, see [[Структура исполняемого файла C++]])

## Call Stack

Every running thread needs a call stack (see [[Call Stack]]). When a process is first run, the kernel creates a single default thread for it. The kernel allocates physical memory pages for this thread’s call stack, and maps them into the process’ virtual address space so the stack can be “seen” by the thread. The values of the stack pointer (SP) and base pointer (BP) are initialized to point to the bottom of the empty stack. Finally, the thread starts executing at the *entry point* of the program. (In C/C++ this is typically main(), or WinMain()
under Windows.)

## Heap

Processes can allocate memory dynamically via `malloc()` and `free()` in C, or
global `new` and `delete` in C++. These requests come from a region of memory
called [[Memory Heap (Куча)|the heap]]. Physical pages of memory are allocated on demand by the
kernel in order to fulfill dynamic allocation requests; these pages are mapped
into the virtual address space of the process as memory is allocated by it, and
pages whose contents have been completely freed are unmapped and returned
to the system.

## Shared Libraries

![[Shared Libraries#Shared Libraries, DLL, PRX]]

## Kernel Pages

On most operating systems, the address space of a process is actually divided into two large contiguous blocks—<mark style="background: #D2B3FFA6;">user space</mark> and <mark style="background: #D2B3FFA6;">kernel space</mark>. For example, on 32-bit Windows, user space corresponds to the address range from address 0x0 through 0x7FFFFFFF (the lower 2 GiB of the address space), while kernel space corresponds to addresses between 0x80000000 and 0xFFFFFFFF (the upper 2 GiB of the space). On 64-bit Windows, user space corresponds to the 8 TiB range of addresses from 0x0 through 0x7FF’FFFFFFFF, and the gigantic 248 TiB range from 0xFFFF0800’00000000 through 0xFFFFFFFF’FFFFFFFF is reserved for use by the kernel (although not all of it is actually used).

User space is mapped through a virtual page table that is unique to each process. However, kernel space uses a separate virtual page table that is shared between all processes. This is done so that all processes in the system have a consistent “view” of the kernel’s internal data.

Normally, user processes are prevented from accessing the kernel’s pages—if they try to do so, a page fault will occur and the program will crash. However, when a user process makes a system call, a context switch (see Section 4.4.6.5) is performed into the kernel. This puts the CPU into privileged mode, allowing the kernel to access the kernel space address ranges (as well as the virtual pages of the current process). The kernel runs its code in privileged mode, updates its internal data structures as necessary, and finally puts the CPU back into user mode and returns control to the user program. For more details on how user and kernel space memory mapping works under Windows, search for “virtual address spaces” on https://docs.microsoft.com.

It’s interesting (and a bit frightening!) to note that the recently-discovered “Meltdown” and “Spectre” exploits make use of a CPU’s [[Out-of-Order Execution|out-of-order]] and [[Speculative Execution|speculative execution]] logic (respectively) to trick it into accessing data located in
memory pages that are normally protected from a user-mode process. For
more on these exploits and how operating systems are protecting themselves
against them, see https://meltdownattack.com/.


# Example Process Memory Map

![[Pasted image 20221127161049.png]]
This figure depicts the memory map of a process as it might look under 32-bit Windows. All of the process’s virtual pages are mapped into user space— the lower 2 GiB of the address space. The executable files’ text, data and BSS segments are mapped at a low memory address, followed by the heap in a higher range, followed by any shared memory pages. The call stack is mapped at the high end of the user address space. Finally, the operating system’s kernel pages are mapped into the upper 2 GiB of the address space. The actual addresses for each of the regions in the memory map aren’t predictable. This is partly because each program’s segments are of different sizes and hence will map to different address ranges. Also, the numeric values of the addresses actually change between runs of the same executable program, thanks to a security measure known as [[Address Space Layout Randomization|address space layout randomization (ASLR)]].