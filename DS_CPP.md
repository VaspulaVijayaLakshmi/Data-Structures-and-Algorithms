-> List (std::list)
Doubly linked list -> (Internal DS)
No random access (no [])



-> Deque (std::deque)
Double-ended queue
Fast insertion/deletion at both ends



-> Queue (std::queue)
FIFO (First In First Out)
Internally uses deque


-> Set (std::set)
Sorted, unique collection (Red-Black Tree)
O(log n) for insert/search.



-> Multiset (std::multiset)
Like set but allows duplicates.
Sorted order
O(log n) for insert/search



-> Unordered Set (std::unordered_set)
Like set, but unsorted
Uses hashing, so average O(1) insert/search


-> Map (std::map)
Stores key-value pairs
Sorted keys (Red-Black Tree)
O(log n) operations


-> Unordered Map (std::unordered_map)
Hash table implementation
O(1) average for insert/search
No order guarantee
Key order doesn't matter








