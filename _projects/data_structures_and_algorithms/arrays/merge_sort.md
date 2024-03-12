---
title: Merge Sort
description: Lorem ipsum dolor sit amet
layout: nested
---

# Merge Sort

 - Divide and conquer
 - Consists of two steps: split array into n single arrays taking `log_2(n)` levels, then merge using two pointers
 - Stable sorting algorithm

 ```python
def mergeSort(arr: list[int], s: int, e: int) -> list[int]:
    if e - s + 1 <= 1:
        return arr
    m = (s + e) // 2

    mergeSort(arr, s, m)
    mergeSort(arr, m + 1, e)

    merge(arr, s, m, e)

def merge(arr: list[int], s: int, m: int, e: int) -> list[int]:
    L = arr[s : m + 1]
    R = arr[m + 1 : e + 1]

    i = 0 # index for L
    j = 0 # index for R
    k = s # index for arr

    while i < len(L) and j < len(R):
        if L[i] <= R[j]:
            arr[k] = L[i]
            i += 1
        else:
            arr[k] = R[j]
            j += 1
        k += 1

    # one of the halfs will have elements remaining
    while i < len(L):
        arr[k] = L[i]
        i += 1
        k += 1
    while j < len(R):
        arr[k] = R[j]
        j += 1
        k += 1
 ```

Time complexity: `O(nlogn)`
