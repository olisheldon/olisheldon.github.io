---
title: Sliding Window
description: INCOMPLETE
layout: nested
---

# Fixed-Length Sliding Window

Question: Given an array of integer, are there two values with a contiguous subarray of size k that are equal?

## Brute Force

This can be solved in a brute-force manner:

```python
def brute_force(nums: list[int], k: int) -> bool:
    for l in range(len(nums)):
        for r in range(l + 1, min(len(nums), l + k)):
            if nums[l] == nums[r]:
                return True
    return False
```
Time complexity: O(N * k)

## Fixed-Length Sliding Window Implementatino

```python
def sliding_window(nums: list[int], k: int) -> bool:
    vals_within_window = set()
    l = 0

    for r in range(len(nums)):
        if r - l + 1 > k:
            vals_within_window.remove(nums[l])
            l += 1
        if nums[r] in vals_within_window:
            return True
        vals_within_window.add(nums[r])

    return False
```

Time complexity: O(n)

# Variable-Length Sliding Window

## Example 1

Question: What is the length of the longest contiguous subarray such that all values within the subarray have the same value?

```python
def longest_subarray(nums: list[int]) -> int:
    length = 0
    l = 0
    
    for r in range(len(nums)):
        if nums[l] != nums[r]:
            l = r 
        length = max(length, r - l + 1)
    return length
```
Time complexity: O(n)

## Example 2

Question: What is the length of the shortest contiguous subarray such that the sum of the values within the subarray are greater than or equal to a given target integer? You can assume that all values are positive

```python
def shortest_subarray(nums: list[int], target: int) -> int:
    l, total = 0, 0
    length = -1
    
    for r in range(len(nums)):
        total += nums[r]
        while total >= target:
            length = min(r - l + 1, length)
            total -= nums[l]
            l += 1
    return 0 if length == -1 else length
```

Time complexity: O(n)
