---
title: Arrays
description: Binary Search, Quick Sort, Merge Sort, Insertion Sort, Bucket Sort
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


# Bucket Sort

 - Unique in that it runs in `O(n)`
 - Constraint: values to sort are within known range
 - [ 2, 1, 2, 0, 0, 2] -> [2, 1, 3], where index represents value and value represents number of occurences
 - Certainly not stable

 ```python
def bucketSort(arr: list[int], known_range: int) -> list[int]:
    counts = [0] * known_range
    for n in arr:
        counts[n] += 1

    i = 0
    for num in range(len(counts)):
        for _ in range(counts[num]):
            arr[i] = num
            i += 1

    return arr
 ```

