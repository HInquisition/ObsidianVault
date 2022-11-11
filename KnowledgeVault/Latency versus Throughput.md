# Latency versus Throughput in Pipelining

The **latency** of a pipeline is the amount of time required to completely process a single instruction. This is just the sum of the latencies of all the stages in the pipeline. Denoting latencies with the time variable $T$, we can write:
$$T_{pipeline} = \sum^{N-1}_{i = 0}\limits{T_i}$$
for a pipeline with $N$ stages.

The **throughput** or bandwidth of a pipeline is a measure of how many instructions
it can process per unit time. The throughput of a pipeline is determined
by the latency of its slowest stage—much as a chain is only as strong as its
weakest link. The throughput can be thought of as a frequency $f$ , measured
in instructions per second. It can be written as follows:
$$f = \frac{1}{\max{T_i}}$$