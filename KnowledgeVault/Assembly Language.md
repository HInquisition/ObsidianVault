# Assembly Language
Writing a program directly in [[Machine Language]] is tedious and error-prone. To make life easier for programmers, a simple text-based version of machine language was developed called **assembly language.** In assembly language, each instruction within a given CPU’s [[ISA, Instruction Set Architecture|ISA]] is given a mnemonic—a short English word
or abbreviation that is much easier to remember than corresponding numeric
[[Opcode]]. 

Instruction operands can be specified conveniently as well: [[Registers]] can be referred to by name (e.g., R0 or EAX), and memory addresses can be written in hex, or assigned symbolic names much like the global variables of higher-level languages. Locations in the assembly program can be tagged with human readable labels, and jump/branch instructions refer to these labels rather than to raw memory addresses.

An assembly language program consists of a sequence of instructions, each
comprised of a mnemonic and zero or more operands, listed in a text file with
one instruction per line. A tool known as an assembler reads the program
source file and converts it into the numeric [[Machine Language|ML]] representation understood by
the [[CPU]]. 