---
title: "Day 4: Ceres Search"
description: Word Search & Pattern Matching <br/> Difficulty ★★
layout: nested
---

<style>
g { color: Green }
</style>

# Day 4: Ceres Search

[**link**](https://adventofcode.com/2024/day/4)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day4.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day4.py)

## Description

This problem involves finding patterns in a word search grid. In part 1, we need to find all instances of "XMAS" in any direction (horizontal, vertical, or diagonal). In part 2, we need to find a specific X-shaped pattern formed by two instances of "MAS".

## Part 1

The solution uses recursive depth-first search to find all instances of "XMAS" in the grid. For each position in the grid, we check all eight possible directions (horizontal, vertical, and diagonal) to see if "XMAS" can be formed starting from that position. The recursive function `word_found` keeps track of:
- Current position (r, c)
- Current character index in "XMAS"
- Direction of search (dr, dc)

The base case is reached when we've found all characters of "XMAS". We use Python's range checks to ensure we stay within grid boundaries.

## Part 2

Part 2 requires finding X-shaped patterns where each diagonal of the X contains "MAS" (forward or backward). The solution checks each position that could be the center of an X (avoiding edges) and verifies if:
1. The center position contains 'A'
2. The four endpoints of the X contain 'M' and 'S' in valid combinations

This is implemented efficiently by checking the center 'A' first and then validating the diagonal patterns. Each X-pattern is counted only once by anchoring on its center position.

## Improvements

### Algorithms

The part 1 solution is O(N * M * D * L) where:
- N, M are grid dimensions
- D is number of directions (8)
- L is length of "XMAS" (4)

Part 2 is O(N * M) as it only needs to check each possible center position once.

The time complexity could potentially be improved for part 1 using pattern matching algorithms like KMP or Aho-Corasick, but given the small input size and word length, the current solution is sufficiently efficient.

### Software Engineering

Some potential improvements:
1. Extract grid boundary checks into a helper function
2. Create a Grid class to encapsulate the 2D array operations
3. Add type hints for better code clarity
4. Consider using `@dataclass` for structured pattern definitions

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday4.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>