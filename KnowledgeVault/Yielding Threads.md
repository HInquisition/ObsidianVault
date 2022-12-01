# Yielding [[Threads]]

This technique falls part-way between [[Polling Threads|polling]] and [[Blocking Threads|blocking]]. The thread polls the condition in a loop, but on each iteration it relinquishes the remainder of its time slice by calling `pthread_yield()` (POSIX), `Sleep(0)` or `SwitchToThread()` (Windows), or an equivalent system call.

Here’s an example:

```C++
// wait for condition to become true
while (!CheckCondition())
{
	// yield the remainder of my time slice
	pthread_yield(nullptr);
}
// the condition is now true and we can continue...
```

This approach tends to result in fewer wasted cycles and better power consumption than a pure busy-wait loop.

Yielding the CPU still involves a [[Kernel Calls|kernel call]], and is therefore quite expensive. Some CPUs provide a lightweight “pause” instruction. (For example, on an Intel x86 [[ISA, Instruction Set Architecture|ISA]] with [[SSE2]], the `_mm_pause()` intrinsic emits such an instruction.) This kind of instruction reduces the power consumption of a busy-wait loop by simply waiting for the CPU’s instruction pipeline to empty out before allowing execution to continue:

```C++
// wait for condition to become true
while (!CheckCondition())
{
// Intel SSE2 only:
// reduce power consumption by pausing for ~40 cycles
_mm_pause();
}
// the condition is now true and we can continue...
```

