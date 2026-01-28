# What is a Heap?
A heap is a tree data structure (most often a binary tree) that keeps the ***extreme*** element at the root
- **Min-heap:** every node is greater than or equal to its parent. ***minimum*** at the root.
- **Max-heap:** every node is less than or equal to its parent. ***maximum*** at the root.

## Two key properties of heaps:
- **Heap-order property:** parent is always ≤ (min-heap) or ≥ (max-heap) its children.
- **Shape property:** it’s a **complete** binary tree (filled level by level, left to right).

## Lower-level implementation: we store that complete tree in a **flat array** (very cache-friendly).
- With 0-based indexing:
	- parent(i) = (i-1)//2
	- left(i) = 2*i + 1
	- right(i) = 2*i + 2
- Insertion uses **sift-up** (bubble the new node up until order holds).
- Deleting the root uses **sift-down** (move the last element to root and push it down to the right spot).

# How does this relate to a priority queue?
- A **priority queue (PQ)** is an **abstract data type**: “give me the next item with the highest priority.”  
- A **heap** is the most common **implementation** of a PQ because it supports:
	- insert(item, priority) → O(log n)
	- extract_min/max() → O(log n)
	- peek() → O(1)

Other PQ implementations exist (e.g., balanced BSTs, binomial/Fibonacci heaps, sorted lists), but binary heaps are the usual sweet spot in practice.

# When do I use a heap / PQ?
- **Scheduling / simulation**: next event with the earliest timestamp.
- **Graph algorithms**: Dijkstra’s / A* frontier.
- **Top-k** from a stream (keep a bounded heap).
- **Merging k sorted lists** (always pick the smallest current head).
- **Anytime you need “give me the next best” efficiently.**

# Pros and cons
**Pros**
- Simple, small constant factors, array-backed.
- Fast O(1) peek, O(log n) insert/pop, O(n) heapify.
- Great for top-k and streaming.
**Cons**
- No fast search or delete of arbitrary element.
- Not globally sorted.
- “Decrease-key” isn’t built-in in many libraries (including Python’s `heapq`).


