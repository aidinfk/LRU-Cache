LRU Cache Implementation in Python
1. The Cache Problem
In many software systems, accessing data from the main source (database, disk, or remote service) is expensive in terms of time and resources.
A cache is a limited-size storage layer that keeps frequently accessed data closer to the application to reduce latency and load.
However, since cache capacity is limited, a replacement policy is required to decide which item should be removed when the cache is full.

This repository focuses on one of the most widely used cache replacement strategies: Least Recently Used (LRU).

2. LRU Cache Explained Simply
LRU (Least Recently Used) removes the item that has not been accessed for the longest time.
The core assumption behind LRU is:
If an item was accessed recently, it is more likely to be accessed again in the near future.

Rules:
Every time an item is accessed (get), it becomes the most recently used.
Every time an item is inserted (put), it becomes the most recently used.
When the cache exceeds its capacity, the least recently used item is evicted.

3. Python Implementation Overview
This implementation achieves O(1) time complexity for both get and put operations by combining two data structures:

1. Hash Map (Dictionary)
Maps keys to nodes
Enables constant-time access to cache entries

2. Doubly Linked List
Maintains access order
Allows constant-time removal and insertion of nodes
Design Invariant
The head of the list represents the least recently used item
The tail of the list represents the most recently used item
Dummy head and tail nodes are used to simplify edge cases

3. Time and Space Complexity Analysis
Operation	Time Complexity
get	O(1)
put	O(1)

Why O(1)?
Dictionary lookup is O(1)
Node removal and insertion in a doubly linked list is O(1)

Space Complexity
O(capacity), since the cache stores a fixed number of nodes

4. Limitations of LRU Cache
While LRU is simple and efficient, it is not optimal for all workloads.

Known Weaknesses
Performs poorly under sequential scan workloads
Cannot distinguish between:
Frequently used items
Recently but rarely used items
May suffer from cache thrashing in streaming scenarios
LRU assumes recency implies importance, which is not always true.

5. Alternative Cache Replacement Algorithms
Modern systems often use more advanced strategies:

LFU (Least Frequently Used)
Evicts items with the lowest access frequency
Better for identifying truly “hot” data

ARC (Adaptive Replacement Cache)
Combines LRU and LFU ideas
Dynamically adapts to access patterns

TinyLFU / W-TinyLFU
Uses probabilistic counting
Employed in high-performance caches such as Caffeine

Segmented LRU (SLRU)
Divides cache into probationary and protected segments
Reduces premature eviction of valuable items

6. When Should You Use LRU?
LRU is a good choice when:
Access patterns exhibit temporal locality
Cache size is moderate
Simplicity and predictability are important
Implementation complexity must be minimal
LRU may not be suitable for:
Large-scale streaming workloads
Highly skewed or scan-heavy access patterns
High-throughput distributed systems

Conclusion
LRU Cache is not obsolete.
It is a foundational algorithm that remains relevant, especially as a baseline or educational reference.
However, modern systems often rely on adaptive or hybrid strategies to achieve better performance under complex workloads.

This implementation aims to provide a clear, minimal, and correct reference for understanding how LRU works internally
