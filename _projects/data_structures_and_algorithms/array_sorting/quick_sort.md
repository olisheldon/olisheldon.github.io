---
title: Quick Sort
description: Lorem ipsum dolor sit amet
layout: nested
---

# Quick Sort

 - Divide and conquer
 - Pick random element (usually right-most), and select as pivot
 - Iterate through all values except pivot, if value < pivot, assign to a 'left' array else assign to 'right' array
 - No extra arrays are allocated, so is particularly memory efficient
 - However, the random pivot selection makes the recursion tree larger, `O(n)` in the worst case
 - Stable sorting algorithm

 ```python
def quickSort(arr: list[int], s: int, e: int) -> list[int]:
    if e -s + 1 <= 1:
        return arr

    pivot = arr[e]
    left = s

    for i in range(s, e):
        if arr[i] < pivot:
            arr[left], arr[i] = arr[i], arr[left]
            left += 1
    
    # move pivot between left and right sides
    arr[e] = arr[left]
    arr[left] = pivot

    quickSort(arr, s, left - 1)
    quickSort(arr, left + 1, e)

    return arr
 ```

