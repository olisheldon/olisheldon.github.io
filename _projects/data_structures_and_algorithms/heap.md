---
title: Heap / Priority Queue
description: Binary Heap, Push, Pop, Heapify
layout: nested
---
 
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

 