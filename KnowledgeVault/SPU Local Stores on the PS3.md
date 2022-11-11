#Consoles
# SPU Local Stores on the PS3

The PlayStation 3 is a classic example of a [[Nonuniform Memory Access (NUMA)|NUMA architecture]]. The PS3 contains a single main [[CPU]] known as the **Power processing unit (PPU)**, eight coprocessors known as **synergistic processing units (SPUs)**, and an NVIDIA RSX graphics processing unit ([[GPU]]). The PPU has exclusive access to 256 MiB of main system RAM (with an [[Memory Cache#Memory Cache Hierarchies|L1 and L2 cache]]), the GPU has exclusive access to 256 MiB of video RAM ([[VRAM]]), and each SPU has its own private 256 KiB local store.

The physical address spaces of main RAM, video RAM and the SPUs’ local stores are all totally **isolated** from one another. This means that, for example, the PPU cannot directly address memory in VRAM or in any of the SPUs’ local stores, and any given SPU cannot directly address main RAM, video RAM, or any of the other SPUs’ local stores, only its own local store.

![[Pasted image 20221101135325.png]]