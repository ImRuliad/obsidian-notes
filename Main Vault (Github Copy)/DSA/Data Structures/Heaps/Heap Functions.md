# Building / maintaining the heap

- **`heapify(a)`**  
    Turn list `a` into a valid min-heap **in place**.  
    Cost: **O(n)**.  
    Use when you already have a list and want to start heap operations fast.
    
- **`heappush(a, x)`**  
    Push element `x` onto heap `a`.  
    Cost: **O(log n)**.  
    Use for incremental inserts.
    
- **`heappop(a)`**  
    Pop and return the **smallest** item.  
    Cost: **O(log n)**.  
    Use to repeatedly take the next smallest.
    
- **`heappushpop(a, x)`**  
    Push `x`, then **pop and return the smallest**—done more efficiently than a separate push then pop.  
    Cost: **O(log n)**.  
    Typical use: fixed-size top-k where most new items won’t enter the heap (if `x` is smaller than the current min, it’s immediately returned and the heap stays the same).
    
- **`heapreplace(a, x)`**  
    **Pop the smallest**, then push `x` (always changes the heap).  
    Cost: **O(log n)**.  
    Typical use: fixed-size top-k where you know `x` should replace the current min if it’s larger; keeps heap size constant.