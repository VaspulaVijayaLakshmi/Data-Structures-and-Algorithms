C++ STL Data Structures Cheat Sheet
🔁 std::list
Type: Doubly Linked List

Key Features:

Fast insertion/deletion from both ends and middle

❌ No random access (no [])

Use When: Frequent insert/delete in the middle of the container

🟦 std::deque
Type: Double-Ended Queue

Key Features:

Fast insertion/deletion from both front and back

✅ Supports random access ([])

Use When: Need dynamic array behavior + efficient front operations

📤 std::queue
Type: FIFO Queue

Internal DS: Uses std::deque

Key Features:

Push at back, pop from front

❌ No direct access to elements

Use When: First-in-first-out processing (e.g., BFS, job queues)

📘 std::set
Type: Ordered Set (Balanced BST – Red-Black Tree)

Key Features:

Stores unique elements in sorted order

O(log n) for insert/search/delete

Use When: Need sorted unique elements with efficient lookups

📗 std::multiset
Type: Ordered Set with Duplicates

Internal DS: Red-Black Tree

Key Features:

Stores duplicate elements in sorted order

O(log n) for insert/search

Use When: Need sorted elements and allow duplicates

📙 std::unordered_set
Type: Unordered Set (Hash Table)

Key Features:

Stores unique elements (no duplicates)

Average case O(1) insert/search/delete

❌ Unordered

Use When: Fast lookup without needing order

📕 std::map
Type: Ordered Key-Value Store (Red-Black Tree)

Key Features:

Stores key-value pairs with sorted keys

O(log n) for insert/search/delete

Use When: Need mapping with sorted keys

📒 std::unordered_map
Type: Unordered Key-Value Store (Hash Table)

Key Features:

Stores key-value pairs with no order

Average O(1) insert/search/delete

Use When: Fast lookup, key order not required
