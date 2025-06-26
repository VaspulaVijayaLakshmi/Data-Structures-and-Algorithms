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
