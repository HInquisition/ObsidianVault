# Control Unit, CU
If the [[CPU|CPU]] is the “brains” of the computer, then the control unit (CU) is the
“brains” of the CPU. Its job is to manage the flow of data within the CPU, and
to orchestrate the operation of all of the CPU’s other components.
The CU runs a program by reading a stream of machine language instructions,
decoding each instruction by breaking it into its [[Opcode|opcode]] and operands,
and then issuing work requests and/or routing data to the [[ALU]], [[FPU|FPU]], [[Vector processing unit, VPU|VPU]],
the registers and/or the [[Memory]] as dictated by the current instruction’s opcode. 
In [[Pipelined CPU]] and [[Superscalar CPU]], the CU also contains complex
circuitry to handle [[Branch Prediction|branch prediction]] and the scheduling of instructions
for out-of-order execution.