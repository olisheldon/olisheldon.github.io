---
title: Arrays
description: Two Pointers, Prefix Sum, Kadanes Algorithm, Sliding Windows
layout: nested
---

# Arrays

## Two Pointers

### Palindrome Checking

Question: Is an array a palindrome?

```python
def is_palindrome(word: str) -> bool:
    l, r = 0, len(word) - 1
    while l < r:
        if word[l] != word[r]:
            return False
        l += 1
        r -= 1
    return True
```
Time complexity: O(n)

### Sum Checking

Question: Given a sorted array of integers, what are the indices of two elements (in different positions) such that their sum is equal to the target? Assume there is exactly one solution.


```python
def target_sum(nums: list[int], target: int) -> tuple[int, int]:
    l, r = 0, len(nums) - 1
    while l < r:
        if nums[l] + nums[r] > target:
            r -= 1
        elif nums[l] + nums[r] < target:
            l += 1
        else:
            return l, r
```

Time complexity: O(n)


## Prefix Sum

A prefix array is a contiguous subarray that includes the first element. 

A postfix array is a contiguous subarray that includes the final element.

Question: What is the ideal data structure for querying the sum of a subarray of values?

i.e.
```python
nums = [2, -1, 3, -3, 4]
PrefixSum(nums).range_sum(3, 0) = nums[3] - nums[0] = 1 - 2 = -1
```

```python
class PrefixSum:

    def __init__(self, nums: list[int]):
        self.prefix = []
        total = 0
        for n in nums:
            total += n
            self.prefix.append(total)
        
    def range_sum(self, l: int, r: int) -> int:
        prefix_right = self.prefix[r]
        prefix_left = self.prefix[l]
        return prefix_right - prefix_left
```
Time complexity: 
 - Construct: O(N)
 - Query: O(1)


## Kadanes Algorithm

Properties:
 - Dynamic programming
 - Greedy algorithm

Question: Given an array of integers, what is the largest sum, non-empty contiguous subarray?

### Brute Force

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

### Kadanes Algorithm

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



### Sliding window variation of Kadanes: O(n)

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

## Fixed-Length Sliding Window

Question: Given an array of integer, are there two values with a contiguous subarray of size k that are equal?

### Brute Force

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

### Fixed-Length Sliding Window Implementatino

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

## Variable-Length Sliding Window

### Example 1

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

### Example 2

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
