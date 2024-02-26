---
title: Kadanes Algorithm
description: INCOMPLETE
layout: nested
---

# Kadanes Algorithm

Properties:
 - Dynamic programming
 - Greedy algorithm

Question: Given an array of integers, what is the largest sum, non-empty contiguous subarray?

## Brute Force

We can solve this simply with a brute force approach; iterating over all subarrays, calculating the sum for each and tracking the maximum sum.

```python
def brute_force(nums: list[int]) -> int:
    max_sum = nums[0]

    for i in range(len(nums)):
        cur_sum = 0
        for j in range(i, len(nums)):
            cur_sum += nums[j]
            max_sum = max(max_sum, cur_sum)
    return max_sum
```

Time complexity: O(n^2)

## Kadanes Algorithm

The approach taken in Kadanes algorithm iterates over the array once. For each num in the array, two values are updated:

 - cur_sum: The total sum of previous contiguous elements such that the sum was never negative or zero
 - max_sum: The maximum value of cur_sum


```python
def kadanes(nums: list[int]) -> int:
    max_sum = nums[0]
    cur_sum = 0

    for n in nums:
        cur_sum = max(cur_sum, 0)
        cur_sum += n
        max_sum = max(max_sum, cur_sum)
    return max_sum
```

This simple change changes the time complexity from brute force O(N**2) to O(N).

Time complexity: O(n)



## Sliding window variation of Kadanes: O(n)

What if instead we wanted to return the left and right index of the maximum subarray sum, assuming there's exactly one result (no ties)?

```python
def sliding_window(nums: list[int]) -> tuple[int, int]:
    max_sum = nums[0]
    cur_sum = 0
    max_L, max_R = 0, 0
    L = 0

    for R in range(len(nums)):
        if cur_sum < 0:
            cur_sum = 0
            L = R

        cur_sum += nums[R]
        if cur_sum > max_sum:
            max_sum = cur_sum
            max_L, max_R = L, R 

    return (max_L, max_R)
```