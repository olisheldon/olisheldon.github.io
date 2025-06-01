---
title: "Day 21: Keypad Conundrum"
description: Chain of Robots <br/> Difficulty ★★★
layout: nested
---

# Day 21: Keypad Conundrum

[**link**](https://adventofcode.com/2024/day/21)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day21.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day21.py)

## Description

In this problem, we need to control a chain of robots to input codes on a numeric keypad. Each robot has a directional keypad to control the next robot's arm, and the final robot types on the numeric keypad. We need to find the shortest sequences of directional inputs to type various codes.

## Part 1

For part 1, we have a chain of 3 robots: our directional keypad controls a robot controlling another robot that types on the numeric keypad. We need to find the shortest sequence of inputs that will result in typing five given codes, and calculate a "complexity" value for each code (length of input sequence × numeric value of code).

The solution approach involves:

1. Creating a mapping of button-to-button movements for both keypad types.
2. For the numeric keypad, computing all possible shortest sequences to type each code.
3. Working backwards through the robot chain to find the shortest sequence that produces each desired sequence.

The key insight is that we can precompute all optimal paths between any two buttons on each keypad type, which allows us to break down the problem into manageable subproblems.

## Part 2

Part 2 increases the complexity by extending the chain to 26 robots (25 with directional keypads plus one at the numeric keypad). The core logic remains the same, but we need an efficient way to compute the sequences through such a long chain.

The solution uses dynamic programming with memoization to avoid recomputing the same sequences multiple times. Each level in the chain depends only on the possible sequences at the next level, allowing us to cache and reuse results.

## Solution Analysis

### Algorithm Complexity

The solution uses several key algorithms:

1. **Path Finding**: Uses breadth-first search to find optimal paths between buttons (O(V + E) for each button pair).
2. **Sequence Generation**: For each code, generates all possible optimal sequences (combinations of paths).
3. **Dynamic Programming**: Used in part 2 to efficiently compute sequence lengths through the robot chain.

The main performance optimization comes from:
- Precomputing and caching all optimal paths between buttons
- Using memoization to avoid recomputing sequence lengths
- Filtering out non-optimal sequences early

### Key Data Structures

1. **Keypad Representations**: Using nested lists for both keypads, with None for empty spaces.
```python
NUM_KEYPAD = [
    ["7", "8", "9"],
    ["4", "5", "6"],
    ["1", "2", "3"],
    [None, "0", "A"]
]
DIR_KEYPAD = [
    [None, "^", "A"],
    ["<", "v", ">"]
]
```

2. **Path Cache**: Dictionary mapping button pairs to optimal movement sequences.
```python
seqs = {(u, v): possibilities for u, v in button_pairs}
```

3. **Memoization Cache**: For part 2, caching computed sequence lengths.
```python
@cache
def compute_length(seq, depth=25)
```

### Software Engineering 

The solution demonstrates several good software engineering practices:

1. **Modularity**: Core functionality is broken into focused functions:
   - `compute_seqs()`: Generates optimal paths between buttons
   - `solve()`: Finds sequences for a given target string
   - `compute_length()`: Computes sequence lengths with memoization

2. **Reusability**: The same core functions work for both keypad types and both parts of the problem.

3. **Efficiency**: Uses caching and early filtering to manage computational complexity:
```python
@cache
def compute_length(seq, depth=25):
    if depth == 1:
        return sum(dir_lens[(u, v)] for u, v in zip("A" + seq, seq))
    length = 0
    for x, y in zip("A" + seq, seq):
        length += min(compute_length(subseq, depth -1) for subseq in dir_seqs[(x, y)])
    return length
```

## Improvements

Potential improvements could include:

1. **Parallelization**: The sequence generation could be parallelized for multiple codes.
2. **Memory Optimization**: Currently stores all possible sequences; could generate them lazily.
3. **Alternative Algorithms**: Could explore A* search for path finding between buttons.
4. **Error Handling**: Could add validation for input codes and keypad layouts.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday21.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>