---
title: Binary Tree
description: Insert, Remove, Search, DFS, BFS, Heap
layout: nested
---

# Binary Tree

 - No cycles
 - Each node can have 0, 1 or 2 children
 - A node with no parents is the root node
 - Node with no children are called leaf nodes
 
 A tree is said to be balanced if the following three conditions hold:

 - The height of the left and right tree for any node does not differ by more than 1.
 - The left subtree of that node is also balanced.
 - The right subtree of that node is also balanced.

 ```python
class Node:

    def __init__(self, val: int):
        self.left = None
        self.right = None
        self.val = val

    def set_left(self, left: 'Node') -> None:
        self.left = left

    def set_right(self, right: 'Node') -> None:
        self.right = right
 ```


# Binary Search Tree Insert & Remove

## Insert

 ```python
 def insert(root: Node, val: int) -> None:
    if not root:
        return Node(val)

    if val > root.val:
        root.right = insert(root.right, val)
    if val < root.val:
        root.left = insert(root.left, val)
 ```

 Time complexity: O(h) where h is the height of the tree, O(logN) if balanced.

## Remove

Requires method to find minimum value node:
 ```python
def min_value_node(root: Node) -> Node:
    curr = root
    while curr and curr.left:
        curr = curr.left
    return curr
 ```

There are two cases to consider:

 - 0 or 1 children
 - 2 children

Case 1:


 ```python
def remove(root: Node, val: int) -> None:
    if not root:
        return None

    if val > root.val:
        root.right = remove(root.right, val)
    elif val < root.val:
        root.left = remove(root.left, val)
    else: # Found value
        if not root.left:
            return root.right
        elif not right.right:
            return root.left
        else:
            min_node = min_value_node(root.right)
            root.val = min_node.val
            root.right = remove(root.right, min_node.val)

    return root
 ```

Time complexity O(logN)

# Binary Search Tree

Binary search trees are binary trees with an extra constraint: For all nodes, each node in it's left subtree must have a value less than its own value and vice-versa

Searching is easily implemented with recursion

 ```python
def search(root: Node, target: int) -> bool:
    if not root:
        return False

    if target > root.val:
        return search(root.right, val)
    elif target < root.val:
        return search(root.left, val)
    else:
        return True
 ```

The time complexity is O(logN) if the tree is balanced, where N is the number of nodes within (i.e. size of) the tree, but is more generally O(h) where h is the height of the tree.

The main advantage of binary search over a tree over binary search over an array is that adding values to the data structure is O(logN) compared to O(N).




# Binary Tree

 - No cycles
 - Each node can have 0, 1 or 2 children
 - A node with no parents is the root node
 - Node with no children are called leaf nodes
 
 A tree is said to be balanced if the following three conditions hold:

 - The height of the left and right tree for any node does not differ by more than 1.
 - The left subtree of that node is also balanced.
 - The right subtree of that node is also balanced.

 ```python
class Node:

    def __init__(self, val: int):
        self.left = None
        self.right = None
        self.val = val

    def set_left(self, left: 'Node') -> None:
        self.left = left

    def set_right(self, right: 'Node') -> None:
        self.right = right
 ```


# Breadth-First Search

Not suited to recursion. We use a queue (FIFO) instead.

 ```python
 def bfs(root: Node) -> None:
    queue = deque()

    if root:
        queue.append(root)

    level = 0
    while len(queue) > 0:
        print(f"level {level}") # this tracking of level is unnecessary for BFS
        for i in range(len(queue)): # but it can be useful
            curr = queue.popleft()
            print(curr.val)
            if curr.left:
                queue.append(curr.left)
            if curr.right:
                queue.append(curr.right)
        
        level += 1
 ```

Set and Map data structures can be implemented using binary search trees.



# Depth-First Search

Uses recursion.

 ```python
 def inOrder(root: Node) -> None:
    if not root:
        return
    
    inOrder(root.left)
    print(root.val)
    inOrder(root.right)
 ```
 ```python
 def preOrder(root: Node) -> None:
    if not root:
        return
    
    print(root.val)
    inOrder(root.left)
    inOrder(root.right)
 ```
 ```python
 def postOrder(root: Node) -> None:
    if not root:
        return
    
    inOrder(root.left)
    inOrder(root.right)
    print(root.val)
 ```

 
# Heap / Priority Queue

The heap / priority queue is a data structure that holds allows constant time access to elements with min or max values (min vs max heaps).

[comment]: <> (treeart, print(binary_edge(14,binary_edge(19, binary_edge(21,65,30),26),binary_edge(16,19,28)))
```
       ╭───14─────╮   
   ╭──19───╮    ╭16──╮
 ╭21──╮   26   19   28
65   30               
```

## Binary Heap

Binary heaps have two properties:

 - Structure: A binary heap is a complete binary tree. Every level is completely filled except perhaps the final level. Nodes in the binary tree *MUST* be added left to right.
  - Order: The min / max value is at the root. Therefore, we require that, for all nodes, all nodes in node.left subtree are greater than or equal to node.val, and all nodes in node.right subtree are greater than or equal to node.val. 

Heaps permit duplicate values. Despite being commonly drawn as trees, binary heaps are actually implemented as vectors. 

```
[ x, 14, 19, 16, 21, 26, 18, 28, 65, 30 ]
[ x,  1,  2,  3,  4,  5,  6,  7,  8,  9 ]
```

Left child = 2i
Right child = 2i + 1
parent = i // 2

This is possible due to the structure property.

|   Operation   | Find-max  | Delete-max |Insert      |Increase-Key|    Meld    |
|---------------|-----------|------------|------------|------------|------------|
|Time complexity|    O(1)   |   O(logN)  |   O(logN)  |   O(logN)  |     O(N)   |


## Heap Push / Pop

### Push

When we push we need to ensure the structure & order properties are maintained.

[comment]: <> (treeart, print(binary_edge(14,binary_edge(19, binary_edge(21,65,30),binary_edge(17,26,0)),binary_edge(16,19,28))))
```
       ╭───14─────╮                    ╭─────14──────╮
   ╭──19───╮    ╭16──╮    -->     ╭───19──────╮      ╭16──╮
 ╭21──╮   26   19   28          ╭21──╮   new╭17     19   28
65   30                        65   30     26   
```

Since we replaced 19 with an even smaller value, we need not look at the left subtree.

We still need to check the order property of the parent however: 19 > 14 so order property is valid.

```python
class Heap:
    def __init__(self):
        self.heap: list[int] = [0]

    def push(self, val: int) -> None:
        self.heap.append(val)

        i = len(self.heap) - 1

        # Percolate up
        while self.heap[i] < self.heap[i // 2]:
            self.heap[i], self.heap[i // 2] = self.heap[i // 2], self.heap[i]

            i = i // 2
```

The push time complexity is O(h) = O(logN).

## Pop

More complicated than push

The naive approach would be to remove the root node and replace it with a smaller child. This would be done recursively, but this breaks the structure property

The actual approach is to pop the root and replace with the last value in the array. This preserves the structure but breaks the order property. Therefore, we must percolate down afterwards.


```python
class Heap:
    ~~~~

    def pop(self) -> int:
        if len(self.heap) == 1:
            return None
        if len(self.heap) == 2:
            return self.heap.pop()

        res: int = self.heap[1]
        self.heap[1] = self.heap.pop()
        i = 1

        # Percolate down
        while 2*i < len(self.heap): # we have at least a left-child
            if 2*i + 1 > len(self.heap)
            and self.heap[2*i + 1] < self.heap[2*i]
            and self.heap[i] > self.heap[2*i + 1]:
                # swap right child
                self.heap[i], self.heap[2*i + 1] = self.heap[2*i + 1], self.heap[i]
                i = 2*i + 1
            elif self.heap[i] > self.heap[2*i]:
                # swap left child
                self.heap[i], self.heap[2*i] = self.heap[2*i], self.heap[i]
                i = 2*i
            else:
                break
        return res
```

The time complexity is O(logN).

## Heapify

Heapify(Array(non-ordered-items)) -> Binary Heap in O(N) time.


```python
class Heap:
    ~~~~

    def heapify(self, arr: list[int]) -> list[int]:
        # 0-th position is moved to the end as we leave the first position 'empty'
        heap: list[int] = []
        heap.append(arr[0])

        cur = (len(arr) - 1) // 2
        while cur > 0:
            # Percolate down
            i = cur
            while 2 * i < len(arr):
                if (2 * i + 1 < len(arr) and 
                arr[2 * i + 1] < arr[2 * i] and 
                arr[i] > arr[2 * i + 1]):
                    # swap right child
                    arr[i], arr[2*i + 1] = arr[2*i + 1], arr[i]
                elif arr[i] > arr[2 * i]:
                    # swap left child
                    arr[i], arr[2*i] = arr[2*i], arr[i]
                    i = 2 * i
                else:
                    break
            cur -= 1
        return heap
```

The time complexity of heapify is O(N).

How is this O(N) when it looks O(NlogN)? Percolating down is very efficient. Only around half of the nodes are in the last level. These can not be percolated down. The next level up has n/4 nodes, then n/8 nodes at the next level and so on. This leads to linear time complexity.

Heaps can also sort data structures. This seems to have provided a sorting algorithm in linear time, however each pop requires O(logN) to preserve heap structure in underlying array, so time complexity of sort is actually O(NlogN). 

## Summary 

Advantages:

 - Get min / max in constant time
 - Build in linear time
 - Sort in O(NlogN)

 Disadvantages:

 - Can't search for random element in O(NlogN) because we can not utilize divide and conquer

 
