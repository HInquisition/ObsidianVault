# Task versus Data [[Parallelism]]

Another way to understand parallelism is to divide it into two broad categories based on the kind of work being done in parallel.

- Task parallelism. When multiple heterogeneous operations are performed in parallel, we call this task parallelism. Performing animation calculations on one core while performing collision checks on another would be an example of this form of parallelism.

- Data parallelism. When a single operation is performed on multiple data items in parallel, it is called data parallelism. Calculating 1000 skinning matrices by running 250 matrix calculations on each of four cores would be an example of data parallelism. Most real concurrent programs make use of both task and data parallelism to varying degrees.