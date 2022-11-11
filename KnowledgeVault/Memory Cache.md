# Memory Cache

PASTE HERE SOME BASICS

## Memory Cache Hierarchies

A memory cache hierarchy is one of the primary mechanisms for mitigating the impacts of high memory access latencies in today’s personal computers and game consoles. In a cache hierarchy, a small but fast bank of [[RAM]] called the **level 1 (L1) cache** is placed very near to the [[CPU]] core (on the same die). Its access latency is almost as low as the CPU’s [[Register Files|||register file]], because it is so close to the CPU core. Some systems provide a larger but somewhat slower **level 2 (L2) cache**, located further away from the core (usually also on-chip, and often shared between two or more cores on a multicore CPU). Some machines even have larger but more-distant L3 or L4 caches. These caches work in concert to automatically retain copies of the most frequently-used data, so that accesses to the very large but very slow bank of main RAM located on the system motherboard are kept to a minimum.

A caching system improves memory access performance by keeping local copies in the cache of those chunks of data that are most frequently accessed by the program. If the data requested by the CPU is already in the cache, it can be provided to the CPU very quickly—on the order of tens of cycles. This is called a **[[Cache hit]]**. If the data is not already present in the cache, it must be fetched into the cache from main RAM. This is called a **[[Cache miss]]**. Reading data from main RAM can take hundreds of cycles, so the cost of a cache miss is very high indeed.

## Cache Lines
 
![[Cache lines#Cache lines]]

## Mapping Cache Lines to Main RAM Addresses

There is a simple **one-to-many** correspondence between memory addresses in the cache and memory addresses in main [[RAM]]. We can think of the address space of the cache as being “mapped” onto the main RAM address space in a repeating pattern, starting at address 0 in main RAM and continuing on up until all main RAM addresses have been “covered” by the cache. 

As a concrete example, let’s say that our cache is 32 KiB in size, and that [[Cache lines]] are 128 bytes each. The cache can therefore hold 256 cache lines ($256 * 128 = 32,768$ B = 32 KiB). Let’s further assume that main RAM is 256 MiB in size. So main RAM is 8192 times as big as the cache, because $(256 * 1024)/32 = 8192$. That means we need to overlay the address space of the cache onto the main RAM address space 8192 times in order to cover all possible physical memory locations. Or put another way, a single line in the cache maps to 8192 distinct line-sized chunks of main RAM. Given any address in main RAM, we can find its address in the cache by taking the main RAM address modulo the size of the cache. So for a 32 KiB cache and 256 MiB of main RAM, the cache addresses `0x0000` through `0x7FFF` (that’s 32 KiB) map to main RAM addresses `0x0000` through `0x7FFF`. But this range of cache addresses also maps to main RAM addresses `0x8000` through `0xFFFF`, `0x10000` through `0x17FFF`, `0x18000` through `0x1FFFF` and so on, all the way up to the last main RAM block at addresses `0xFFF8000` through `0xFFFFFFF`. 

![[Pasted image 20221030162519.png]]

## Addressing the Cache

Let’s consider what happens when the [[CPU]] reads a single byte from memory. The address of the desired byte in main [[RAM]] is first converted into an address within the cache. The cache controller then checks whether or not the [[Cache lines|cache line]] containing that byte already exists in the cache. If it does, it’s a [[Cache hit]], and the byte is read from the cache rather than from main RAM. If it doesn’t, it’s a [[Cache miss]], and the line-sized chunk of data is read from main RAM and loaded into the cache so that subsequent reads of nearby addresses will be fast.

The cache can only deal with memory addresses that are aligned to a multiple of the cache line size (see [[Memory Alignment]]). Put another way, the cache can really only be addressed in units of lines, not bytes. Hence we need to convert our byte’s address into a cache line index.

Consider a cache that is $2^M$ bytes in total size, containing lines that are $2^n$ in size. The $n$ least-significant bits of the main RAM address represent the offset of the byte within the [[Cache lines|cache line]] . We strip off these $n$ least-significant bits to convert from units of bytes to units of lines (i.e., we divide the address by the cache line size, which is $2^n$). Finally we split the resulting address into two pieces: The $(M - n)$ least significant bits become the cache line index, and all the remaining bits tell us from which cache-sized block in main RAM the [[Cache lines|cache line]] came from. The block index is known as the <mark style="background: #D2B3FFA6;">tag</mark>.

In the case of a [[Cache miss]], the cache controller loads a line-sized chunk of data from main RAM into the corresponding line within the cache. The cache also maintains a small **table of tags**, one for each cache line. This allows the caching system to keep track of from which main RAM block each line in the cache came. This is necessary because of the **many-to-one relationship** between memory addresses in the cache and memory addresses in main RAM. 

![[Pasted image 20221030163636.png]]

Returning to our example of reading a byte from main RAM, the complete sequence of events is as follows: 
1. The [[CPU]] issues a read operation. 
2. The main [[RAM]] address is converted into an offset, line index and tag. 
3. The corresponding tag in the cache is checked, using the line index to find it. 
	- If the tag in the cache matches the requested tag, it’s a **[[Cache hit]].** In this case, the line index is used to retrieve the line-sized chunk of data from the cache, and the offset is used to locate the desired byte within the line. 
	- If the tags do not match, it’s a **[[Cache miss]]**. In this case, the appropriate line-sized chunk of main RAM is read into the cache, and the corresponding tag is stored in the cache’s tag table. Subsequent reads of nearby addresses (those that reside within the same cache line) will therefore result in much faster cache hits.

## Set Associativity and Replacement Policy

The simple mapping between [[Cache lines]] and main [[RAM]] addresses described above is known as a **direct-mapped cache**. It means that each address in main RAM maps to only one line in the cache. Using our 32 KiB cache with 128- byte lines as an example, the main RAM address ``0x203`` maps to cache line 4 (because ``0x203`` is 515, and $⌊515/128⌋ = 4$). However, in our example there are 8192 unique cache-line-sized blocks of main RAM that all map to cache line 4. Specifically, cache line 4 corresponds to main RAM addresses ``0x200`` through `0x27F`, but also to addresses `0x8200` through `0x827F`, and `0x10200` through `0x1027f`, and 8189 other cache-line-sized address ranges as well.

When a **[[Cache miss]]** occurs, the [[CPU]] must load the corresponding [[Cache lines|cache line]] from main memory into the cache. If the line in the cache contains no valid data, we simply copy the data into it and we’re done. But if the line already contains data (from a different main memory block), we must overwrite it. This is known as <mark style="background: #D2B3FFA6;">evicting the cache line</mark>.

The problem with a direct-mapped cache is that it can result in pathological cases. For example, two unrelated main memory blocks might keep evicting one another in a ping-pong fashion. We can obtain better average performance if each main memory address can map to two or more distinct lines in the cache. In a **2-way set associative cache**, each main RAM address maps to two cache lines. Obviously a 4-way set associative cache performs even better than a 2-way, and an 8-way or 16-way cache can outperform a 4-way cache and so on.

![[Pasted image 20221030171743.png]]

Once we have more than one “cache way,” the cache controller is faced with a dilemma: When a cache miss occurs, which of the “ways” should we evict and which ones should we allow to stay resident in the cache? The answer to this question differs between CPU designs, and is known as the CPU’s [[Cache Replacement Policy]]. One popular policy is **not most-recently used (NMRU)**. In this scheme, the most-recently used “way” is kept track of, and eviction always affects the “way” or “ways” that are not the most-recently used one. Other policies include **first in first out (FIFO)**, which is the only option in a direct-mapped cache, **least-recently used (LRU)**, **least frequently used (LFU)**, and pseudorandom.

## Multilevel Caches

The **hit rate** is a measure of how often a program hits the cache, as opposed to incurring the large cost of a [[Cache miss]]. The higher the hit rate, the better the program will perform (all other things being equal). There is a fundamental trade-off between **cache latency** and **hit rate**. The larger the cache, the higher the hit rate—but larger caches cannot be located as close to the CPU, so they tend to be slower than smaller ones.

Most game consoles employ at least two levels of cache. The [[CPU]] first tries
to find the data it’s looking for in the level 1 (L1) cache. This cache is small
but has a very low access latency. If the data isn’t there, it tries the larger but higher-latency level 2 (L2) cache. Only if the data cannot be found in the L2 cache do we incur the full cost of a main memory access. Because the latency of main RAM can be so high relative to the CPU’s clock rate(see [[The Memory Gap]]), some PCs even include level 3 (L3) and level 4 (L4) caches.

## Instruction Cache and Data Cache

When writing high-performance code for a game engine or for any other
performance-critical system, it is important to realize that both data and code are cached. The **instruction cache** (**[[I-cache]]**, often denoted I\$) is used to preload executable machine code before it runs, while the **data cache** (**[[D-cache]]**, or D\$) is used to speed up read and write operations performed by that machine code. In a level 1 (L1) cache, the two caches are always physically distinct, because it is undesirable for an instruction read to cause valid data to be bumped out of the cache or vice versa. So when optimizing our code, we must consider both **D-cache** and **I-cache** performance (optimizing one tends to have a positive effect on the other). Higher-level caches (L2, L3, L4) typically do not make this distinction between code and data, because their larger size tends to mitigate the problems of code evicting data or data evicting code.

## Write Policy

We haven’t talked yet about what happens when the [[CPU]] writes data to [[RAM]]. How the cache controller handles writes is known as its **write policy**. The simplest kind of cache is called a <mark style="background: #D2B3FFA6;">write-through cache</mark>; in this relatively simple cache design, all writes to the cache are mirrored to main RAM immediately. In a <mark style="background: #D2B3FFA6;">write-back</mark> (or copy-back) cache design, data is first written into the cache and the cache line is only flushed out to main RAM under certain circumstances, such as when a dirty cache line needs to be evicted in order to read in a new cache line from main RAM, or when the program explicitly requests a flush to occur.

## Cache Coherency: MESI, MOESI and MESIF

When multiple [[CPU]] cores share a single main memory store, things get more
complicated. It’s typical for each core to have its own L1 cache, but multiple
cores might share an L2 cache, as well as sharing main RAM.

![[Pasted image 20221030184942.png]]

In the presence of multiple cores, it’s important for the system to maintain <mark style="background: #D2B3FFA6;">cache coherency</mark>. This amounts to making sure that the data in the caches belonging to multiple cores match one another and the contents of main RAM. Coherency doesn’t have to be maintained at every moment—all that matters is that the running program can never tell that the contents of the caches are out of sync.

The three most common cache coherency protocols are known as [[MESI]] (modified, exclusive, shared, invalid), MOESI (modified, owned, exclusive, shared, invalid) and MESIF (modified, exclusive, shared, invalid and forward)


## Avoiding Cache Misses

Obviously [[Cache miss|cache misses]] cannot be totally avoided, since data has to move to and from main RAM eventually. The trick to writing high performance software in the presence of a memory cache hierarchy is to arrange your data in RAM, and design your data manipulation algorithms, in such a way that the minimum number of cache misses occur. 

The best way to avoid [[D-cache]] misses is to organize your data in contiguous blocks that are as small as possible and then access them sequentially. When the data is contiguous (i.e., you don’t “jump around” in memory a lot), a single cache miss will load the maximum amount of relevant data in one go. When the data is small, it is more likely to fit into a single [[Cache lines|cache line]] (or at l east a minimum number of cache lines). And when you access your data sequentially, you avoid evicting and reloading cache lines multiple times.

Avoiding [[I-cache]] misses follows the same basic principle as avoiding [[D-cache]] misses. However, the implementation requires a different approach. The easiest thing to do is to keep your high-performance loops as small as possible in terms of code size, and avoid calling functions within your innermost loops. If you do opt to call functions, try to keep their code size small too. This helps to ensure that the entire body of the loop, including all called functions, will remain in the [[I-cache]] the entire time the loop is running.

Use inline functions judiciously. Inlining a small function can be a big performance boost. However, too much inlining bloats the size of the code, which can cause a performance-critical section of code to no longer fit within the cache.
See [[Inline Functions]]