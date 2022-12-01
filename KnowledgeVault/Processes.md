# Processes

A process is the operating system’s way of managing a running instance of a program contained in an executable file (.exe on Windows, .elf on Linux). A process only exists while its program is actually running—when an instance of a program exits, is killed, or crashes, the OS destroys the process associated with that instance. Multiple processes can be running on a computer system at any given time. This might include multiple instances of the same program.

Programmers interact with processes via an API provided by the operating system. The details of this API differ from OS to OS, but the key concepts are roughly the same across all of them. 

![[Anatomy of a Process]]

[[Virtual Memory Map of a Process]]