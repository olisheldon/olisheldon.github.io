---
title: "Day 1: Pairing Points"
description: Minimizing point distances<br/> <br/> Difficulty ★★
layout: nested
---

# Day 1: Pairing Points

[**link**](https://adventofcode.com/2024/day/1)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day1.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day1.py)

## Description

The first problem of Advent of Code 2024 involves processing pairs of numbers and finding optimal pairings or matches between them.

## Part 1

In part 1, we need to find the absolute difference between corresponding pairs of numbers from two sequences. The solution uses a heap-based approach to efficiently process the numbers:

1. Two min-heaps are maintained: one for left values and one for right values
2. Numbers are pushed into their respective heaps
3. Numbers are popped from both heaps simultaneously to compute differences
4. The sum of all differences is returned

The use of heaps ensures we're always working with the smallest available numbers from each sequence.

## Part 2

Part 2 changes the approach by looking for matching pairs. Instead of finding differences, we need to count how many times each number appears in both sequences. The solution uses:

1. A list for left values (maintaining order)
2. A defaultdict for right values to count occurrences
3. For each left value, multiply it by its count in the right sequence

This approach efficiently handles the counting and matching of values between sequences.

## Implementation Details

```python
def part1():
    left = []
    right = []

    for l, r in values:
        heapq.heappush(left, l)
        heapq.heappush(right, r)

    res = 0
    while left and right:
        res += abs(heapq.heappop(left) - heapq.heappop(right))
    assert(len(left) == len(right) == 0)
    return res

def part2():
    left, right = [], defaultdict(int)

    for l, r in values:
        left.append(l)
        right[r] += 1
    
    res = 0
    for l in left:
        res += l * right[l]
    return res
```

## Algorithmic Analysis

### Part 1
- Time Complexity: O(n log n) due to heap operations
- Space Complexity: O(n) for storing values in heaps

### Part 2
- Time Complexity: O(n) for both building the count dictionary and processing left values
- Space Complexity: O(n) for storing the dictionary and list

## Improvements

Several potential improvements could be made:

1. Memory optimization: The current solution stores all values in memory. For very large inputs, we could process values in chunks.

2. Early termination: If we know certain conditions about the input data, we might be able to stop processing early.

3. Parallelization: For very large datasets, the counting in part 2 could potentially be parallelized.

4. Input validation: The current solution assumes well-formed input. Adding validation could make it more robust.

## Software Engineering

The solution follows good software engineering practices:

1. Clean separation between parts 1 and 2
2. Use of appropriate data structures (heapq for ordered processing, defaultdict for counting)
3. Clear variable names and logical structure
4. Assertion to verify assumptions about the data
5. Modular file handling separate from core logic