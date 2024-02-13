---
title: Bucket Sort
description: Lorem ipsum dolor sit amet
layout: nested
---

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

