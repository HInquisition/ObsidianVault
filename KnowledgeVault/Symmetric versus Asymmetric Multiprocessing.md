# Symmetric versus Asymmetric Multiprocessing

The symmetry of a parallel computing platform has to do with how the CPU  cores in the machine are treated by the operating system. 

![[SMP, Symmetric Multiprocessing#SMP, Symmetric Multiprocessing]]

The PlayStation 4 and the Xbox One are examples of SMP. Both of these consoles contain eight cores, of which seven are available for use by the programmer, and the application is free to run threads on any of the available cores.

![[AMP, Asymmetric Multiprocessing#AMP, Asymmetric multiprocessing]]

The cell broadband engine (CBE) used in the PlayStation 3 is an example of AMP; it employs a main CPU known as the “power processing unit” (PPU) which is based on the PowerPC [[ISA, Instruction Set Architecture|ISA]], along with eight coprocessors known as “synergystic processing units” (SPUs) which are based around a completely different ISA. (See [[SPU Local Stores on the PS3]] for more on the PS3’s hardware architecture.)