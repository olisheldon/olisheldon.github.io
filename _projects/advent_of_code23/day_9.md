---
title: "Day 9: Mirage Maintenance"
description: Extrapolation <br/> Difficulty ★
layout: nested
---

# Day 9: Mirage Maintenance

[**link**](https://adventofcode.com/2023/day/9)

[**input**](https://adventofcode.com/2023/day/9/input)

[**code**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day9.py)

## Description

This problem requires generating new sequences from a given sequence of values. The elements of the new sequences are the difference between each previous element. This process is repeated until the sequence is all zeros.

```
Input:  10  13  16  21  30  45  68 
          3   3   5   9  15  23 |
            0   2   4   6   8   |
              2   2   2   2     | 
                0   0   0       V 
```

## Part 1

Once a full sequence has been built, extrapolate the values to the right hand side. We must return the sum of these extrapolated values.

This problem lends itself to an easy implementation using recursion:

```python
def extrapolate(subhistory: list[int]) -> int:
    # Base case
    if all(val == 0 for val in subhistory):
        return 0
    
    # Calculate new sequence and recursively call
    deltas: list[int] = [y - x for x, y in zip(subhistory, subhistory[1:])]
    diff: int = extrapolate(deltas)
    
    # Pop back up stack returning value of interest
    return subhistory[-1] + diff
```

## Part 2

Part 2 asks us to instead extrapolate to the left hand side. We must again return the summ these extrapolated values.

It was very simple to modify part 1 to achieve this:

```python
def extrapolate(subhistory: list[int], forwards: bool = True) -> int:
    if all(val == 0 for val in subhistory):
        return 0
    
    deltas: list[int] = [y - x for x, y in zip(subhistory, subhistory[1:])]
    diff: int = extrapolate(deltas, forwards)
    
    if not forwards:
        return subhistory[0] - diff
    return subhistory[-1] + diff
```

## Improvements

My solution using recursion is a nice solution to the problem, but in way optimal in time or space complexity.

I am sure that this problem has a constant time solution, but will be

 - Difficult to understand for someone reading the code
 - Less adaptable (the change from part 1 to part 2 would have been much more work)

### Algorithms

Use of recursion makes solution very concise.

### Software Engineering
