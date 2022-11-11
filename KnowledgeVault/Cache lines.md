# Cache lines

Memory caching takes advantage of the fact that memory access patterns in real software tend to exhibit two kinds of locality of reference:
1. **Spatial locality**. If memory address $N$ is accessed by a program, it’s likely that nearby addresses such as $N + 1$, $N + 2$ and so on will also be accessed. Iterating sequentially through the data stored in an array is an example of a memory access pattern with a high degree of spatial locality.
2. **Temporal locality**. If memory address $N$ is accessed by a program, it’s likely that that same address will be accessed again in the near future. Reading data from a variable or data structure, performing a transformation on it, and then writing an updated result into the same variable or data structure is an example of a memory access pattern with a high degree of temporal locality.

To take advantage of locality of reference, memory caching systems move data into the cache in contiguous blocks called <mark style="background: #D2B3FFA6;">Cache lines</mark> rather than caching data items individually.
 
For example, let’s say the program is accessing the data members of an instance of a class or struct. When the first member is read, it might take hundreds of cycles for the [[Memory controller]] to reach out into main [[RAM]] to retrieve the data. However, the cache controller doesn’t just read that one member—it actually reads a larger contiguous block of RAM into the cache. That way, subsequent reads of the other data members of the instance will likely result in low-cost [[Cache hit|cache hits]].


