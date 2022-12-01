# Context Switching

Every [[Threads|thread]] maintained by the kernel exists in one of three states:
- *Running*. The thread is actively running on a core.
- *Runnable*. The thread is able to run, but it is waiting to receive a time slice on a core.
- *Blocked*. The thread is asleep, waiting for some condition to become true.

A <mark style="background: #D2B3FFA6;">context switch</mark> occurs whenever the kernel causes a thread to transition from one of these states to another.

A context switch always happens in [[Kernel Mode Privileges|privileged mode]] on the CPU—in response to the [[Hardware Interrupts|hardware interrupt]] that drives [[Preemptive Multitasking]] (i.e., transitions between Running and Runnable), in response to an explicit blocking [[Kernel Calls|kernel call]] made by a running thread (i.e., a transition from Running or Runnable to Blocked), or in response to a waited-on condition becoming true, thus “waking” a sleeping thread (i.e., transitioning it from Blocked to Runnable). The kernel’s thread state machine is illustrated in this figure:

![[Pasted image 20221129194754.png]]

When a thread is in the Running state, it is actively making use of a CPU core. The core’s [[Registers]] contain information pertinent to the execution of that thread, such as its instruction pointer (IP), stack and base pointers (SP and BP), and the contents of various general-purpose registers (GPRs). The thread also maintains a call stack, which stores local variables and return addresses for the currently-running function and the entire stack of functions that ultimately called it. Together, this information is known as the <mark style="background: #D2B3FFA6;">thread’s execution context</mark>.

Whenever a thread transitions away from the Running state to either Runnable or Blocked, the contents of the CPU’s registers are saved to a memory block that has been reserved for the thread by [[The Kernel]]. Later, when a Runnable thread transitions back to the Running state, the kernel repopulates the CPU’s registers with that thread’s saved register contents.

We should note here that a thread’s [[Call Stack|call stack]] need not be saved or restored explicitly during a context switch. This is because each thread’s call stack already resides in a distinct region within its process’ virtual memory map. The act of saving and restoring the contents of the CPU’s registers includes saving and restoring the stack and base pointers (SP and BP), and thereby effectively saves and restores the thread’s call stack “for free.”

During a context switch, if the incoming thread resides in a different process from that of the outgoing thread, the kernel also needs to save off the state of the outgoing process’ virtual memory map, and set up the virtual memory map of the incoming process. [[Virtual Memory|A virtual memory map]] is defined by a virtual page table. The act of saving and restoring a virtual memory map therefore involves saving and restoring a pointer to this page table, which is usually maintained in a special privileged CPU register. The [[Translation Lookaside Buffer, TLB|translation lookaside buffer (TLB)]] must also be flushed whenever an inter-process context switch occurs. These additional steps make context switching between processes more expensive than context switching between threads within a single process.