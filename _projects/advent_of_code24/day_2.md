---
title: "Day 2: Red-Nosed Reports"
description: Sequence Analysis <br/> Difficulty ★★
layout: nested
---

# Day 2: Red-Nosed Reports

[**link**](https://adventofcode.com/2024/day/2)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day2.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day2.py)

## Description

This problem involves analyzing sequences of numbers to determine if they follow specific patterns. A sequence is considered "safe" if it is either strictly increasing or strictly decreasing, with adjacent numbers differing by at least 1 and at most 3.

## Part 1

The solution leverages Python's zip() function for elegant pairwise comparisons. The safe() function checks two conditions:
1. The sequence is either all increasing or all decreasing (using two all() checks with zip())
2. Adjacent differences are within the required range (using another all() with zip())

This approach avoids manual indexing and provides a clear, functional implementation.

## Part 2

Part 2 introduces the "Problem Dampener" concept, where we can remove one number to potentially make an unsafe sequence safe. The solution uses generator expressions to:
1. Generate all possible sequences with one number removed
2. Check if any of these modified sequences are safe
3. Sum up the total number of sequences that can be made safe

The implementation maintains efficiency by using generators rather than creating full lists of possibilities.

## Improvements

### Algorithms

The current solution has O(n²) complexity for part 2, as we need to check n-1 possible sequences (removing one number each time) for each input sequence. Given the problem constraints, this is unavoidable as we need to try removing each number.

### Software Engineering

The solution demonstrates good use of:
1. Generator expressions for memory efficiency
2. Functional programming concepts with all() and zip()
3. Clean separation of core logic (safe()) from the part-specific implementations

One potential improvement would be to add type hints and docstrings for better code documentation.