---
title: Insertion Sort
description: Lorem ipsum dolor sit amet
layout: nested
---

# Insertion Sort

 - Sort a size-increasing subarray of the original array
 - Iterative algorithm
 - Sort next element with know that preceeding elements are already sorted.
 - Iterative algorithm using pointer
 - Stable sorting algorithm

 ```python
 def insertionSort(arr: list[int]) -> list[int]:
    for i in range(1, len(arr)):
        while j >= 0 and arr[j] > arr[j + 1]:
            arr[j], arr[j + 1] = arr[j + 1], arr[j]
            j -= 1
    return arr
 ```

Best case: `O(n)`
Worst case: `O(n^2)`
