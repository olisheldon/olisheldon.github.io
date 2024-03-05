---
title: Prefix Sum
description: INCOMPLETE
layout: nested
---

# Prefix Sum

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
