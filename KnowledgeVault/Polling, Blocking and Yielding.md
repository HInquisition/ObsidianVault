# Polling, Blocking and Yielding

Normally a thread runs until it terminates. But sometimes a running thread needs to wait for some future event to occur. For example, a thread might need to wait for a time-consuming operation to complete, or for some resource to become available.

In such a situation, we have three options:

1. The thread can [[Polling Threads|poll]],
2. it can [[Blocking Threads|block]], or
3. it can [[Yielding Threads|yield]] while polling.


![[Polling Threads#Polling Threads]]

![[Blocking Threads#Blocking Threads]]

![[Yielding Threads#Yielding Threads]]