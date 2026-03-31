
# Basic heap operations (peek/pop/push)
```python
import heapq

h = [7, 3, 5, 9, 1]
heapq.heapify(h)        # O(n); h becomes a valid min-heap
min_val = h[0]          # peek smallest in O(1)
heapq.heappush(h, 2)    # push new element
smallest = heapq.heappop(h)  # pop smallest (2)

```

# Max-Heap code in python
```python
import heapq

nums = [5, 1, 9, 3]
h = []
for x in nums:
    heapq.heappush(h, -x)   # negate to simulate max-heap

print(-heapq.heappop(h))    # 9
print(-heapq.heappop(h))    # 5
```

# Streaming top-k with a fixed-size heap
```python
import heapq

def top_k(iterable, k):
    it = iter(iterable)
    h = list(sorted([next(it) for _ in range(k)]))  # seed with first k
    heapq.heapify(h)                                # min-heap of current top k
    for x in it:
        if x > h[0]:
            heapq.heapreplace(h, x)                 # pop min, push x
    return sorted(h, reverse=True)                  # top k, largest first

print(top_k([10, 4, 12, 3, 25, 7, 18], 3))  # [25, 18, 12]

```

# Merging k sorted lists
```python
import heapq

a = [1, 4, 10]
b = [2, 3, 8]
c = [0, 9, 11]

merged = list(heapq.merge(a, b, c))  # -> [0,1,2,3,4,8,9,10,11]

```

# Priority queue with tie-breakers
```python
import heapq, itertools

pq = []
counter = itertools.count()  # total ordering for ties

def add_task(task, priority=0):
    heapq.heappush(pq, (priority, next(counter), task))

def pop_task():
    priority, _, task = heapq.heappop(pq)
    return task, priority

```