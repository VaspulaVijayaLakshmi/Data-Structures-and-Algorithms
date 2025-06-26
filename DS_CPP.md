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

---___


##  std::unordered_map (C++ STL)


```cpp
unordered_map<int, string> m;
```

Even though the map is empty at this point, it has already allocated some **initial number of buckets** internally.

---

###  Load Factor

```
Load Factor = size / bucket_count
```

- **`size`** → Number of key-value pairs currently stored in the `unordered_map`.
- **`bucket_count`** → Number of allocated "slots" or "bins" for hashing.

---

### Key Concepts

- On every `insert()`, **a new slot is not created**.
  - Creating buckets is expensive.
  - Instead, the unordered_map starts with a **default bucket count** (usually 8).
- As you insert more items:
  - The `load_factor` increases.
  - Once it crosses a threshold (e.g., 1.0), the map **rehashes**:
    - Increases the number of buckets.
    - Redistributes all existing elements into the new bucket array.

---

###  Example

```cpp
unordered_map<int, int> m;

cout << "Initial size: " << m.size() << endl;
cout << "Initial bucket count: " << m.bucket_count() << endl;

// Sample Output:
// Initial size: 0
// Initial bucket count: 8
```

---

###  Pre-Allocating Buckets

You can **reserve** space in advance to avoid frequent rehashing:

```cpp
unordered_map<int, int> m;
m.reserve(1000);  // Pre-allocate enough buckets for ~1000 elements
```

This improves performance if you know the approximate size.

---

###  Internal Structure

- The underlying **bucket array** is conceptually like a **dynamic array**.
- Each bucket holds a **linked list** (or `forward_list`) of key-value pairs that hash to the same index.

```text


bucket[0] → empty
bucket[1] → (5, "A")
bucket[2] → (18, "B") → (34, "C")  ← collision: separate chaining
bucket[3] → empty
...
```

---

###  Performance

| Operation | Average Time | Worst Case |
|-----------|--------------|-------------|
| Insert    | O(1)         | O(n)        |
| Search    | O(1)         | O(n)        |
| Delete    | O(1)         | O(n)        |

> Worst case happens if all elements hash to the same bucket (bad hash function or malicious input).




###DEQUEUE

## Why does std::deque support random access, even though it's a double-ended queue?

In theoretical data structures, a double-ended queue (deque) only supports fast insertion and deletion at both ends — it does not require random access.

However, `std::deque` in C++ is designed as a practical, flexible container:

- `std::deque` = efficient double-ended operations + fast random access
- It behaves like a hybrid between `std::vector` and `std::list`

---

## std::deque in C++

`std::deque` is more than just a traditional double-ended queue. It is a general-purpose sequence container like `vector`, but optimized differently.

In addition to front/back operations, it supports:

- `operator[]`
- `.at()`
- Iterators with random access capability

---

## How is random access possible?

Internally, `std::deque` is not implemented as:

- A linked list
- A single contiguous array (like `vector`)

Instead, it uses a **map of fixed-size memory blocks**, often called a **segmented array**.

---

### Internal Structure (Conceptual)


```
Map (array of pointers):
+----+----+----+----+
| B1 | B2 | B3 | B4 |
+----+----+----+----+

Each block Bx is a fixed-size array (e.g., 64 elements)
```

---

### How `deque[i]` Works

To access an element by index:

1. Compute which block the index falls into:

```
block_index = i / block_size
```

2. Compute offset within that block:

```
offset_in_block = i % block_size
```

3. Access the element at:

```
map[block_index][offset_in_block]
```




___________________



###QUEUE :

### Summary

- `std::queue` is a **wrapper**, not a new data structure
- Implements FIFO using `std::deque` by default
- No iterators, no random access (`operator[]` is not available)
- Use it when you need a simple queue interface with fast front/back operations

