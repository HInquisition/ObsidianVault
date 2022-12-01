# Joining [[Threads]]

It’s common for one thread to spawn one or more child threads, do some useful work of its own, and then wait for the child threads to be done with their work before continuing. For example, let’s say the main thread wants to perform 1000 computations, and let’s assume further that this program is running on a quad-core machine. The most efficient approach would be to divide the work into four equally-sized chunks, and spawn four threads to do the processing in parallel. Once the computations are complete, let’s assume that the main thread wants to perform a checksum on the results. 

The resulting code might look something like this:

```c++
ComputationResult g_aResult[1000];

void Compute(void* arg)
{
	uintptr_t startIndex = (uintptr_t)arg;
	uintptr_t endIndex = startIndex + 250;
	for (uintptr_t i = startIndex; i < endIndex; ++i)
	{
		g_aResult[i] = ComputeOneResult(...);}
	}
}

void main()
{
	pthread_t tid[4];
	for (int i = 0; i < 4; ++i)
	{
		const uintptr_t startIndex = i * 250;
		pthread_create(&tid[i], nullptr, Compute, (void*)startIndex);
	}
	// perhaps do some other useful work...
	// wait for computations to be done
	for (int i = 0; i < 4; ++i)
	{
		pthread_join(&tid[i], nullptr);
	}
	// all threads are done, so we can do our checksum
	unsigned checksum = Sha1(g_aResult,
	1000*sizeof(ComputationResult));
	// ...
}
```