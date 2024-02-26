---
title: Two Pointers
description: INCOMPLETE
layout: nested
---

# Two Pointers

## Palindrome Checking

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

## Sum Checking

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