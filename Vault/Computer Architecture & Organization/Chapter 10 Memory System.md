## <u> Introduction </u>
*The performance of both Uniform Memory Access (UMA) and Nonuniform Memory Access (NUMA) depends on latency.
Any improvement in latency would increase the bandwidth of the system.
The longer a CPU (processing core) stays idle, the number of clock cycles required to execute programs increases, reducing instruction throughput.
There is no single technology available that can be used to build a low-latency, large-capacity, and low-cost memory.

- SRAM is the fastest and is thus used as cache memory inside the processor, but is also the most expensive.
- [[Chapter 7 Memory#<u> Modern DRAM </u>|DRAM]] costs less, but is slower, requiring access times in the order of 100 CPU cycles.
- Magnetic and flash memory cost the least, but are the slower, about 1,000,000 times slower than CPU.

**A combination of these technologies is usually used in a hierarchical structure, where the fastest is nearest to the CPU and the slowest is furthest away.**
![[Screenshot 2025-11-21 at 5.59.23 PM.png]]
*Data is copied from the lowest level of memory hierarchy to the next higher level until it is at the highest level before they are access by the CPU.*
Multiple data items (such as a block or page) are copied between levels of hierarchy.
The CPU will wait to receive data as long as data is in main memory.
A program's execution will be stopped if the instruction or data the CPU requested is not in the main memory.

##### Data Coherency
While a program is executing, modified data is copied from a higher level to the next lower level of memory hierarchy to create space or to inform the lower-level memory of changes when necessary. For example:
- Consider a data item at memory address X that is copied from main memory to L2 cache.
- Data is then copied from L2 Cache to L1 Cache before it is access by CPU.
- CPU operates on data item, writing new values.
- OS instructs a direct memory access (DMA) controller to transfer data, including data at address X, from main memory to hard disk.

To prevent stale data from ever being saved on disk or ever being access by CPU, certain ***Data Coherency*** protocols must be implemented between levels in memory hierarchy.
Because volatile memory access time is very small (in the order of 100 CPU cycles max), the task of copying and maintaining coherency between memory levels, except between the lowest two levels in the hierarchy, must be performed in hardware.

Copying and maintaining data coherency between nonvolatile memory ***(Virtual Memory)*** and volatile memory ***(Physical Memory)*** requires certain functions to be performed in hardware and others to be performed in software.
A virtual memory management system decides where in the ***physical memory*** to store the codes and data of one or more programs stored on the hard disk.

## <u> Memory Hierarchy </u>
- DRAM technologies (typically [[Chapter 7 Memory#<u> Modern DRAM </u>|SDRAMs]]), are used to build a large main (physical) memory.
- SRAM technologies are used to build small but fast cache memories inside the processor.

