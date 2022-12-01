# Software Interrupts

A software interrupt is triggered by software rather than by a voltage on a CPU pin (like [[Hardware Interrupts]]). It has the same basic effect as a hardware interrupt, in that it causes the operation of the CPU to be interrupted and a service routine to be called. A software interrupt can be triggered explicitly by executing an “interrupt” [[Machine Language|machine language]] instruction. Or one may be triggered in response to an erroneous condition detected by the CPU while running a piece of software—these are called *traps* or sometimes *exceptions* (although the latter term should not be confused with language-level exception handling). For example, if an [[ALU]] is instructed to perform a divide-by-zero operation, a software interrupt will be raised. The operating system normally handles such interrupts by crashing the program in question and producing a [[Core Dump|core dump]] file. However, a debugger attached to the program could catch this interrupt and instead cause the program to break into the debugger for inspection.