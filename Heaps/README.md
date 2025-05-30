What is a Heap?
A Heap is a special tree-based data structure primarily used to implement priority queues. It is represented as a Binary Tree, where each node has at most two children. Specifically, Heaps are complete binary trees, meaning all levels are completely filled except possibly the last, which is filled from left to right.

Heaps can be efficiently represented using an array, where indices correspond to positions in the binary tree.

_____________________________________________


Array Representation
For a node at index i:

-> Root node: i = 0 (first element of the array)

Parent node: parent(i) = ⌊(i - 1) / 2⌋
-> Left child: left(i) = 2i + 1
-> Right child: right(i) = 2i + 2

O-based Indexing


________________________________________________



Types of Heaps:

-> Min Heap: The parent node is less than or equal to its children. The smallest element is at the root.
-> Max Heap: The parent node is greater than or equal to its children. The largest element is at the root.


__________________________________________


Common Heap Use Cases 


-> Top K Pattern

-> Finding the top K largest/smallest elements.
Examples: Kth largest number, Top K frequent elements.

-> Merge K Sorted Lists Pattern
Efficiently merge multiple sorted lists or arrays.


-> Two Heaps Pattern
Useful in problems like finding the median from a stream of numbers.


->Minimum Number Pattern
Problems involving task scheduling, meeting rooms, etc., where minimum values are frequently accessed.
