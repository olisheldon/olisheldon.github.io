---
title: Binary Search
description: Lorem ipsum dolor sit amet
layout: nested
---

# Binary Search

 - Divide and conquer
 - Requires sorted data structure

 ```python
def binarySearch(arr: list[int], target: int) -> int:
    l, r = 0, len(arr) - 1

    while l <= r:
        m = (l + r) // 2

        if target > arr[mid]:
            l = mid + 1
        elif target < arr[mid]:
            r = mid - 1
        else:
            return mid
    
    return -1
 ```

