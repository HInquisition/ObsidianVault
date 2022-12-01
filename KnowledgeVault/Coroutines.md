# Coroutines

Coroutines are a particular type of [[User-Level Threads|user-level thread]] that can prove very useful for writing inherently asynchronous programs, like web servers—and games! A coroutine is a generalization of the concept of a *subroutine*. Whereas a subroutine can only exit by returning control to its caller, a coroutine can also exit by [[Yielding Threads|yielding]] to another coroutine. When a coroutine yields, its [[Context Switching|execution context]] is maintained in memory. The next time the coroutine is called (by being yielded to by some other coroutine) it continues from where it left off.

Subroutines call each other in a hierarchical fashion. Subroutine A calls B, which calls C, which returns to B, which returns to A. But coroutines call each other symmetrically. Coroutine A can yield to B, which can yield to A, ad infinitum. This back and forth calling pattern doesn’t lead to an infinitely deepening call stack, because each coroutine maintains its own private execution context (call stack and register contents). Thus yielding from coroutine A to coroutine B acts more like a context switch between threads than like a function call. But because coroutines are implemented with user-level threads, these context switches are very efficient.

Here’s a pseudocode example of a system in which one coroutine continually produces data that is consumed by another coroutine:
```C++
Queue g_queue;
coroutine void Produce()
{
	while (true)
	{
		while (!g_queue.IsFull())
		{
			CreateItemAndAddToQueue(g_queue);
		}
		YieldToCoroutine(Consume);
		// continues from here on next yield...
	}
}
coroutine void Consume()
{
	while (true)
	{
		while (!g_queue.IsEmpty())
		{
			ConsumeItemFromQueue(g_queue);
		}
		YieldToCoroutine(Produce);
		// continues from here on next yield...
	}
}
```

The C++ Boost library provides a solid implementation of coroutines, but Boost requires you to compile and link against a pretty huge codebase. If you want something leaner, you may want to try rolling your own coroutine library. The following blog post by Malte Skarupke demonstrates that doing so isn’t quite as onerous a task as you might at first imagine: https://probablydance.com/2013/02/20/handmade-coroutines-for-windows/.