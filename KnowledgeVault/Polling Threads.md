# Polling [[Threads]]

<mark style="background: #D2B3FFA6;">Polling</mark> involves a thread sitting in a tight loop, waiting for a condition to become true. It’s a bit like kids in the back seat on a road trip, repeatedly asking, “Are we there yet? Are we there yet?” Here’s an example:

```c++
// wait for condition to become true
while (!CheckCondition())
{
// twiddle thumbs
}
// the condition is now true and we can continue...
```

It should be obvious that this approach, while simple, has the potential of burning CPU cycles unnecessarily. This approach is sometimes called a <mark style="background: #D2B3FFA6;">spin-wait</mark> or a busy-wait.
