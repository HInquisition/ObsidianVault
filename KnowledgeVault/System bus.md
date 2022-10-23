# System [[Bus|Bus]]

The system bus combines the functions of the three main buses:

-   The **control bus** carries the control, timing and coordination signals to manage the various functions across the system.
  
-   The **[[Address Bus]]** is used to specify memory locations for the data being transferred.
  
-   The **data bus**, which is a bidirectional path, carries the actual data between the processor, the memory and the peripherals.

The [[CPU]] loads data from a memory cell into one of its [[Registers|registers]] by supplying an
address to the [[Memory controller]] via the address bus. The memory controller
responds by presenting the bits of the data item stored in the cell(s) in question
onto the data bus, where it can be “seen” by the [[CPU]]. Likewise, the [[CPU]]
writes a data item to memory by broadcasting the destination address over the
address bus and placing the bit pattern of the data item to write onto the data
bus. The [[Memory controller]] responds by writing the given data into the corresponding memory cell(s). 

The design and dimensions of the system bus are based on the specific processor technology of the motherboard. For example, system bus can be implement as physically separated 3 buses or as 1 wide united bus.