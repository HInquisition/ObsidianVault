# The Memory Gap

In the early days of computing, memory access latency and instruction execution latency were on roughly equal footing. For example, on the Intel 8086, [[Registers]]-based instructions could execute in two to four cycles, and a main memory access also took roughly four cycles. However, over the past few decades both raw [[Clock]] speeds and the effective instruction throughput of [[CPU]]s have been improving at a much faster rate than memory access speeds. Today, the access latency of main memory is extremely high relative to the latency of executing a single instruction: Whereas a [[Registers]]-based instruction still takes between one and 10 cycles to complete on an Intel Core i7, an access to main [[RAM]] can take on the order of 500 cycles to complete! This ever-increasing discrepancy between [[CPU]] speeds and memory access latencies is often called the memory gap. 

![[Pasted image 20221025195342.png]]
