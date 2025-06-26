## C++ STL Containers Reference

### std::list
- Doubly linked list (internal data structure)
- No random access (no [] operator)
- Fast insertion/deletion at beginning, middle, end

### std::deque
- Double-ended queue
- Fast insertion/deletion at both ends
- Supports random access (operator[])

### std::queue
- FIFO (First In First Out)
- Push at back, pop from front
- No random access
- Internally uses std::deque

### std::set
- Stores unique elements
- Sorted order (internally Red-Black Tree)
- O(log n) for insert/search/delete

### std::multiset
- Like std::set, but allows duplicate elements
- Sorted order
- O(log n) for insert/search/delete

### std::unordered_set
- Stores unique elements
- No order maintained
- Uses hash table internally
- Average O(1) for insert/search/delete
- Worst-case O(n) in case of hash collisions

### std::map
- Stores key-value pairs
- Keys are unique and sorted
- Internally implemented as Red-Black Tree
- O(log n) for insert/search/delete

### std::unordered_map
- Stores key-value pairs
- Keys are unique, no order maintained
- Internally uses hash table
- Average O(1) for insert/search/delete
- Worst-case O(n) if many hash collisions



_____________________________________________




##  std::set (C++ STL)

- **Implemented as**: Balanced Binary Search Tree (usually a Red-Black Tree)

###  Properties:
- Stores **unique** elements
- Elements are stored in **sorted (ascending)** order
- Time complexity: `O(log n)` for insert, delete, and search

###  Internals:
Each node in the Red-Black Tree contains:
- `key`
- `color` (red or black)
- `left`, `right`, and `parent` pointers

Balanced trees (like Red-Black Trees) **keep height low**, ensuring operations stay efficient (logarithmic).

---

##  std::unordered_map (C++ STL)

```cpp
unordered_map<int, string> m;




___________________________________



###Unordered_map


unordered_map<int, string> m;

At this point, even though it's empty, the unordered map has already allocated some initial number of buckets.


Load Factor = size / bucket_count


What is size?
size = Number of key-value pairs currently stored in the unordered_map.


What is bucket_count?
bucket_count = Number of available buckets (i.e., "slots" or "bins" in the internal hash table array).


So each time we insert an element the new slot is not added , becaise its an expensive oepration, it would be given some random defaukt size.

Once the size hits or once the load factor hits tht means there are possibilities of collisions, the map rehashes:

It increases bucket_count
Redistributes all existing entries into new buckets


unordered_map<int, int> m;
cout << "Initial size: " << m.size() << endl;
cout << "Initial bucket count: " << m.bucket_count() << endl;



Initial size: 0
Initial bucket count: 8



You can pre-allocate buckets using reserve():

unordered_map<int, int> m;
m.reserve(1000);  // reserve enough buckets for 1000 elements


the underlying bucket array is conceptually similar to a dynamic array



















