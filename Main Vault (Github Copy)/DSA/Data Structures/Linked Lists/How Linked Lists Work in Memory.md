*Unlike Arrays, Linked Lists are stored in memory in fragments*

## <u> Linked Lists in Memory </u>
- Each node is allocated separately via `malloc` or `new` (this happens under the hood in python when new objects are created).
- The memory allocator places these wherever it finds free space (leading to scattered non-contiguous memory locations)

> [!DANGER] Cache Friendliness
> Linked Lists are NOT cache friendly like arrays are because Linked Lists are stored in non contiguous parts of memory. Modern CPUs fetch entire cache lines (typically 64 bytes) and these nodes are likely stored in different cache lines.
