---
title: "Day 1: Historian Hysteria"
description: List comparison and matching <br/> Difficulty ★★
layout: nested
---

# Day 1: Historian Hysteria

[**link**](https://adventofcode.com/2024/day/1)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day1.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day1.py)

## Description

The first problem of Advent of Code 2024 involves helping Elvish Senior Historians reconcile two different lists of location IDs. The Chief Historian has gone missing, and these lists might help track him down - but they don't quite match up.

## Part 1

In part 1, we need to find how different the two lists are by pairing up numbers from each list and calculating their distances. Specifically:

1. Match the smallest number from the left list with the smallest from the right list
2. Continue matching second-smallest with second-smallest, and so on
3. Calculate the absolute difference between each pair
4. Sum up all the differences

The solution uses a heap-based approach to efficiently match numbers by size:

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
```

The use of heaps ensures we're always matching the current smallest numbers from each list, exactly as the problem requires.

## Part 2

Part 2 takes a different approach - instead of looking at differences, we need to find matching numbers between the lists. The theory is that matching numbers are actual location IDs, while differences might be misinterpreted handwriting.

For each number in the left list, we need to:
1. Count how many times it appears in the right list
2. Multiply the number by its count in the right list
3. Sum up all these products

The solution uses a dictionary to efficiently count occurrences:

```python
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
- Time Complexity: O(n log n) due to heap operations for sorting
- Space Complexity: O(n) for storing values in heaps

### Part 2
- Time Complexity: O(n) for building the count dictionary and processing left values
- Space Complexity: O(n) for storing unique values and their counts

## Improvements

Possible improvements to the solution could include:

1. Input validation: The current solution assumes well-formed input with equal-length lists
2. Memory optimization: For very large inputs, we could process values in chunks
3. Early termination: If we know certain properties about the data (e.g., all numbers are unique), we could optimize certain operations

## Software Engineering

The solution demonstrates good practices:

1. Clean separation between parts 1 and 2
2. Appropriate data structures for each task:
   - Heaps for ordered processing in part 1
   - defaultdict for efficient counting in part 2
3. Clear variable names that reflect the problem domain (left/right for the two lists)
4. Assertion to verify assumptions about the input data
5. Modular file handling separate from core logic

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday1.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday1.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>