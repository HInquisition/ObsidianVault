# SDRAM, Synchronous [[DRAM]]
SDRAM is designed to synchronize itself with the timing of the [[CPU|CPU]]. This enables the [[Memory controller]] to know the exact [[Clock]] cycle when the requested data will be ready, so the CPU no longer has to wait between memory accesses.

However, SDRAM transfers data on _one_ edge of the clock. [[DDR]] SDRAM means that this type of SDRAM fetches data on both the leading edge and the falling edge of the clock signal that regulates it