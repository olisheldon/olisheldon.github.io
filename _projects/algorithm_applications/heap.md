---
title: Heap / Priority Queue
description: Median Finding
layout: nested
---

# Heap / Priority Queue

Question: Implement a data structure that can efficiently return the median and dynamically edit the data

Inserting a new value into a sorted array is O(N), then indexing the middle element is O(1). Therefore total time is O(N).

This can be improved to an insertion complexity of O(logN), and indexing of median of O(1).

## Median Finding

Maintain two heaps, one max and one min. Each heap contains half of the elements added so far (maximum difference in heap size of 1). Every value in the min heap should be less than or equal to every value in the max heap. Moving values between the heaps is permitted to maintain equality (within 1) of each heap's size.

Instead of worrying about which heap to put each incoming value into, we can simplify by just always putting the value in the min heap, then compare max heap's max value to min heap's min value. Then move accordingly.

```python
import heapq

class Median:
    def __init__(self):
        self.small: list[float | int] = []
        self.large: list[float | int] = []

    def insert(self, num: int | float) -> None:
        # Push to the max heap and swap with min heap if needed.
        heapq.heappush(self.small, -1 * num)
        if (self.small and self.large and (-1 * self.small[0]) > self.large[0]):
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        
        # Handle uneven size
        if len(self.small) > len(self.large) + 1:
            val = -1 * heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        if len(self.large) > len(self.small) + 1:
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -1 * val)
        
    def get_median(self) -> int | float:
        if len(self.small) > len(self.large):
            return -1 * self.small[0]
        elif len(self.large) > len(self.small):
            return self.large[0]
        
        # Even # of elements, return avg of two middle nums
        return (-1 * self.small[0] + self.large[0]) / 2
```