What is Heap?

It is mainly used to represent a priority queue.
It is represented as a Binary Tree (a tree structure where a node of a tree has a maximum of two child nodes). Heaps are complete binary trees.
A simple array can be used to represent a Heap where array indices refer to the node position in the tree.


Parent and child nodes can be accessed with indices:


A root node｜i = 0, the first item of the array
A parent node｜parent(i) = i / 2
A left child node｜left(i) = 2i
A right child node｜right(i)=2i+1
Two type of Heaps — Min Heap, Max Heap

Min Heap — the parent node always has a smaller value than the child nodes.


Max Heap — the parent node is always larger than the child node value.



