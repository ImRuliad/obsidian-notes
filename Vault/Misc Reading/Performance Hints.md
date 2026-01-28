> [!DANGER] Taken from this reading located here
> https://abseil.io/fast/hints.html


## <u> Certain Operations have different latency </u>

| Operations                        | Latency        |
| --------------------------------- | -------------- |
| L1 Cache Reference                | 0.5 ns         |
| L2 Cache Reference                | 3 ns           |
| Branch Mispredict                 | 5 ns           |
| Mutex Lock/Unlock (contended)     | 15 ns          |
| Main Memory Reference             | 50 ns          |
| Compress 1K bytes with Snappy     | 1,000 ns       |
| Read 4KB from SSD                 | 20,000 ns      |
| Round trip within same datacenter | 50,000 ns      |
| Read 1MB sequentially from memory | 64,000 ns      |
| Read 1MB over 100Gbps network     | 100,000 ns     |
| Read 1MB from SSD                 | 1,000,000 ns   |
| Disk seek                         | 5,000,000 ns   |
| Read 1MB sequentially from disk   | 10,000,000 ns  |
| Send packet CA->Netherlands->CA   | 150,000,000 ns |

---
## <u> Example: Time to Quicksort a Billion 4 Byte Numbers </u>
*Roughly, a good quicksort algo makes log(n) passes over an array of size N. On each pass, the array contents will be streamed from memory into processor cache, the partition code will compare each element once to a pivot element.*

- **Memory Bandwidth**
	- The array occupies 4 GB (4 Bytes/number * 1 Billion numbers). 
	- Assume `~16GB/s` of memory bandwidth per core.
	- Each pass will thus take `~0.25s`. 
	- N is `~2^30`, so it will make `~30` passes.
	- Total cost of memory transfer will be `~7.5s`
- **Branch Mispredictions**
	- A total of N * log(N) comparisons are made i.e. `~30 billion` comparisons.
	- Assume half of them are mispredicted.
	- Multiply `5ns` per misprediction.
	- Total cost of misprediction will be `75` seconds

> [!DANGER] Adding the total cost of mispredictions and memory transfer will result in a total estimate of `~82.5` seconds.

## <u> Example: Time to Generate a Web Page with 30 Image Thumbnails </u>
*Comparing two potential designs where the original images are stored on disk, and each image is approx 1MB in size.*

- Design One
	- Read the contents of the 30 images sequentially and generate a thumbnail for each one. Each read takes one seek (`5ms`) + one transfer (`10ms`) which, which adds up to 30 images times `15ms` per image, `450ms`.
- Design Two
	- Read in parallel, assuming images are spread evenly across `k` disks. The latency above still holds, but will drop by roughly a factor of `k` (We could get unlucky and one disk will have more than `1/Kth` of the images being read). If running on a distributed filesystem with hundreds of disks, expected latency will drop to `~15ms`.

> [!DANGER] Consider a design where all images are on a single SSD. This changes the sequential read performance to `20µs` + `1ms` per image. Adds up to `~30ms` overall.

---
## <u> Measurement </u>
*Before making improvements or running into tradeoffs involving performance, simplicity, etc.. its good to measure or estimate potential performance benefits.*

**Profiling Tools and Tips**
- A useful tool to reach for first is [pprof](https://github.com/google/pprof/blob/main/doc/README.md). It gives a good high level performance info and is easy to use both locally and for code running in prod.
- [perf](https://perf.wiki.kernel.org/index.php/Main_Page) is good for detailed insight into performance.

**Some tips for profiling**
- Build production binaries with appropriate debugging informations and optimization flags.
- If possible, write a [microbenchmark](https://abseil.io/fast/75) that covers the code you are improving. Microbenchmarks improve turnaround time when making performance improvements, help verify the impact of performance improvements, and help prevent future performance regressions. Microbenchmarks have [pitfalls](https://abseil.io/fast/39) that make them non-representative of full system performance. Useful libraries for microbenchmarks [C++](https://github.com/google/benchmark/blob/main/README.md) [Go](https://pkg.go.dev/testing#hdr-Benchmarks) [Java](https://github.com/openjdk/jmh)
- Use a benchmark library to [emit performance counter readings](https://abseil.io/fast/53) both for better precision, and to get more insight into program behavior.

> [!DANGER] Lock contention can often artificially lower CPU usage. Some mutex implementations provide support for profiling lock contention.

**What To Do When Profiles Are Flat**
