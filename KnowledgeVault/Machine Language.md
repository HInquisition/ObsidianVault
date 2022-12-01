# ML, Machine Language
Computers can only deal with numbers. As such, each instruction in a program’s
instruction stream must be encoded numerically. When a program is
encoded in this way, we say it is written in **machine language**, or ML for short.
Of course, machine language isn’t a single language—it’s really a multitude of
languages, one for each distinct [[CPU]] / [[ISA, Instruction Set Architecture]].

Every machine language instruction is comprised of three basic parts:
-  **[[Opcode]]**, which tells the [[CPU]] which operation to perform (add, subtract, move, jump, etc.),
- zero or more operands which specify the inputs and/or outputs of the instruction, and
- some kind of options field, specifying things like the addressing mode of the instruction and possibly other flags.


The [[Opcode]] and operands (if any) of an ML instruction are packed into a
contiguous sequence of bits called an instruction word. A hypothetical [[CPU]]
might encode its instructions with perhaps the first byte containing the opcode, addressing mode and various options flags, followed by some number of bytes for the operands. Each [[ISA, Instruction Set Architecture|ISA]] defines the width of an instruction word (i.e., the number of bits occupied by each instruction) differently. In some [[ISA, Instruction Set Architecture|ISAs]], all instructions occupy a fixed number of bits; this is typical of **reduced instruction set computers ([[RISC]])**. In other [[ISA, Instruction Set Architecture|ISAs]], different types of instructions may be encoded into differently-sized instruction words; this is common in **complex instruction set computers ([[CISC]])**.

Two hypothetical machine language instruction encoding schemes. 
- Top: In a variable width encoding scheme, different instructions may occupy different numbers of bytes in memory ([[CISC]]).
- Bottom: A fixed-width instruction encoding uses the same number of bytes for every instruction in an instruction stream ([[RISC]])

![[Pasted image 20221014164953.png]]

Instruction words can be as small as four bits in some microcontrollers, or
they may be many bytes in size. Instruction words are often multiples of 32 or
64 bits, because this matches the width of the [[Registers|CPU’s registers]] and/or [[System bus|data bus]].
In **very long instruction word ([[VLIW]])** CPU designs, parallelism is achieved by
allowing multiple operations to be encoded into a single very wide instruction
word, for the purpose of executing them in parallel. Instructions in a [[VLIW]]
[[ISA, Instruction Set Architecture|ISA]] can therefore be upwards of hundreds of bytes in width.