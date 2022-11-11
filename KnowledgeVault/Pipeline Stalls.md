# [[Pipelined CPU|Pipeline]] Stalls 

Sometimes the CPU is unable to issue a new instruction on a particular clock
cycles. This is called a **stall**. On such a clock cycle, the first stage in the pipeline
lies idle. On the next clock cycle, the second stage will be idle, and so on. A
stall can therefore be thought of as a “bubble” of idle time that propagates
through the pipeline at a rate of one stage per clock cycle. These bubbles are
sometimes called <mark style="background: #D2B3FFA6;">delay slots</mark>.