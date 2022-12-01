# Thread Priorities and Affinity

For the most part, [[The Kernel]] handles the job of scheduling [[Threads]] to run on the available cores in the machine. However, programmers do have two ways to affect how threads are scheduled: <mark style="background: #D2B3FFA6;">priority</mark> and <mark style="background: #D2B3FFA6;">affinity</mark>.

A thread’s *priority* controls how it is scheduled relative to other Runnable threads in the system. Higher-priority threads generally take precedence over lower-priority threads. Different operating systems offer different numbers of priority levels. For example, Windows threads can belong to one of six priority classes, and there are seven distinct priority levels within each class. These two values are combined to produce a total of 42 distinct “base priorities” which are used when scheduling threads.

The simplest thread scheduling rule is this: As long as at least one higher-priority Runnable thread exists, no lower-priority threads will be scheduled to run. The idea behind this approach is that most threads in the system will be created at some default priority level, and hence will share the processing resources fairly. But once in a while, a higher-priority thread can become Runnable. When it does, it runs as close to immediately as possible, hopefully exits after a relatively short period of time, and thereby returns control to all of the lower-priority threads.
 
Such a simple priority-based scheduling algorithm can lead to a situation in which a small number of high-priority threads run continually, thereby preventing any lower-priority threads from running. This is known as <mark style="background: #D2B3FFA6;">starvation</mark>. Some operating systems attempt to mitigate the ill effects of starvation by introducing exceptions to the simple scheduling rule that aim to give at least some CPU time to starving lower-priority threads.

Another way in which programmers can control thread scheduling is via a thread’s *affinity*. This setting requests that the kernel either lock a thread to a particular core, or that it should at least prefer one or more cores over the others when scheduling the thread.