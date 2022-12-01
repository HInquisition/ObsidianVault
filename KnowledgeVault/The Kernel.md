# The Kernel

Modern operating systems handle a wide variety of tasks, across a wide range of granularities. These range from the handling of keyboard and mouse events or the scheduling of programs for [[Preemptive Multitasking]] at one end of the spectrum, to managing a printer queue or the network stack at the other end. The “core” of the operating system—the part that handles all of the most fundamental and lowest-level operations—is called <mark style="background: #D2B3FFA6;">the kernel</mark>. The rest of the operating system, and all user programs, are built atop the services provided by the kernel.

![[Pasted image 20221125154833.png]]
*The kernel and device drivers sit directly on top of the hardware, and run in [[Kernel Mode Privileges|privileged mode]]. All other operating system software and all user programs are implemented on top of the kernel and driver layer, and run in a somewhat restricted user mode.*