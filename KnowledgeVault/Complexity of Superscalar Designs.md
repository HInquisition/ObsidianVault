# Complexity of Superscalar designs

Implementing a [[Superscalar CPU]] isn’t quite as simple as “copying and pasting” two identical CPU cores onto a die. Although it’s reasonable to envision a superscalar CPU as two parallel instruction [[Pipelined CPU|pipelines]], these two pipelines are fed from a single instruction stream. Some some kind of control logic is therefore required at the front end of these parallel pipes. Just as on a CPU that supports [[Out-of-Order Execution]], a superscalar CPU’s control logic looks ahead in the instruction stream in an attempt to identify dependencies between instructions, and then issues instructions out of order in an attempt to mitigate their effects.

In addition to [[Data Dependencies|data]] and [[Branch Dependencies|branch]] dependencies, a superscalar CPU is prone to a third kind of dependency known as a [[Resource Dependencies|resource dependency]]. 
![[Resource Dependencies#Resource dependency]]
As such, the control logic that manages instruction dispatch on a superscalar CPU is even more complex than that found on a scalar CPU that supports out-oforder execution.