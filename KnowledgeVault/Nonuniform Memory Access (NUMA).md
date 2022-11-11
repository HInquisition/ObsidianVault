# Nonuniform Memory Access (NUMA)

When designing a multiprocessor game console or personal computer, system architects must choose between two fundamentally different memory architectures: **uniform memory access (UMA)** and **nonuniform memory access (NUMA)**. 

In a UMA design, the computer contains a single large bank of main [[RAM]] which is visible to all [[CPU]] cores in the system. The physical address space looks the same to each core, and each can read from and write to all memory locations in main RAM. A UMA architecture typically makes use of a [[Memory Cache#Memory Cache Hierarchies|cache hierarchy]] to mitigate memory access latency issues.

One problem with a UMA architecture is that the cores often contend for access to main RAM and any shared caches. For example, the PS4 contains eight cores arranged into two clusters. Each core has its own private L1 cache, but each cluster of four cores shares a single L2 cache, and all cores share main RAM. As such, the cores often contend with one another for access to the L2 cache and main RAM.

One way to address core contention problems is to employ a **non-uniform memory access (NUMA)** design. In a NUMA system, each core is provided with a relatively small bank of high-speed dedicated RAM called a <mark style="background: #D2B3FFA6;">local store</mark>. Like an L1 cache, a local store is typically located on the same die as the core itself, and is only accessible by that core. But unlike an L1 cache, access to the local store is explicit. A local store might be mapped to part of a core’s address space, with main RAM mapped to a different range of addresses. Alternatively, certain cores might only be able to see the physical addresses within its local store, and might rely on a **direct memory access controller** ([[DMAC]]) to transfer data between the local store and main RAM.

Examples of NUMA architecture:
- [[SPU Local Stores on the PS3]]
- [[PS2 Scratchpad (SPR)]]