# DRAM, Dynamic Random Access [[Memory]]
DRAM - Main [[RAM]] memory of PC, cheaper, has higher density compared to [[SRAM]].

DRAM needs to be “refreshed” periodically (by reading the data and then re-writing it) in order to prevent its contents from disappearing. This is because DRAM memory cells are built from MOS capacitors that gradually lose their charge, and reading such memory cells is destructive to the data they contain. 

Originally, DRAM was not regulated by a [[Clock]]. DRAM was asynchronous, i.e., not synchronized by any external influence. This posed a problem in organizing data as it comes in so it can be queued for the process it’s associated with. Because DRAM was asynchronous, it was not going to work as fast with processors that were just getting faster. [[SDRAM]] is synchronous, creating predictable orderly cycles of data fetches and writes.

Some subtypes and specifications of DRAM:
- [[SDRAM]] - Synchronous DRAM
- [[DDR]] - Double Data Rate Synchronous memory.

