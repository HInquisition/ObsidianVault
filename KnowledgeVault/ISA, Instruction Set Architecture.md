# ISA, Instruction Set Architecture

[[CPU]] designs vary widely from one manufacturer to the next. The set of all
instructions supported by a given [[CPU]], along with various other details of the
CPU’s design like its addressing modes and the in-memory instruction format,
is called its **instruction set architecture** or **ISA**. (This is not to be confused with
a programming language’s application binary interface or ABI, which defines
higher-level protocols like calling conventions.) 

The following categories of instruction types are common to pretty much every ISA:

- **Move**. These instructions move data between [[Registers]], or between [[Memory]] and a register. Some ISAs break the “move” instruction into separate “load” and “store” instructions.
- **Arithmetic operations**. These of course include addition, subtraction, multiplication and division, but may also include other operations like unary negation, inversion, square root, and so on.
- **Bitwise operators**. These include AND, OR, exclusive OR (abbreviated XOR or EOR) and bitwise complement.
- **Shift/rotate operators**. These instructions allow the bits within a data word to be shifted left or right, with or without affecting the carry bit in the status register, or rotated (where the bits rolling off one end of the word “wrap around” to the other end).
- **Comparison**. These instructions allow two values to be compared, in order to determine if one is less than, greater than or equal to the other. In most CPUs, the comparison instructions use the [[ALU]] to subtract the two input values, thereby setting the appropriate bits in the status register, but the result of the subtraction is simply discarded.
- **Jump and branch**. These allow program flow to be altered by storing a new address into the instruction pointer. This can be done either unconditionally (in which case it is called a “jump” instruction) or conditionally based on the state of various flags in the status register (in which case it is often called a “branch”). For example, a “branch if zero” instruction alters the contents of the IP if and only if the “Z” bit in the status register is set.
- **Push and pop**. Most CPUs provide special instructions for pushing the contents of a [[Registers|register]] onto the [[Call Stack]] and for popping the current value at the top of the stack into a register.
- **Function call and return**. Some ISAs provide explicit instructions for calling a function (also known as a procedure or subroutine) and returning from it. However, function call and return semantics can also be provided by a combination of push, pop and jump instructions.
-  **[[Interrupts]]**. An “interrupt” instruction triggers a digital signal within the [[CPU]] that causes it to jump temporarily to a pre-installed interrupt service routine routine which is often not part of the program being run. Interrupts are used to notify the operating system or a user program of events such as an input becoming available on a peripheral device. Interrupts can also be triggered by user programs in order to “call” into the operating system kernel’s routines. 
- **Other instruction types**. Most ISAs support a variety of instruction types that don’t fall into one of the categories listed above. For example, the “no-op” instruction (often called NOP) is an instruction that has no effect other than to introduce a short delay. NOP instructions also consume memory, and on some ISAs they are used to align subsequent instructions properly in memory