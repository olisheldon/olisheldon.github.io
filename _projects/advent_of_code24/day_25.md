---
title: "Day 25: Code Chronicle"
description: Array Processing & Pattern Matching <br/> Difficulty ★★
layout: nested
---

# Day 25: Code Chronicle

[**link**](https://adventofcode.com/2024/day/25)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day25.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day25.py)

## Description

For this day's problem we are presented with schematics of locks and keys for a virtual five-pin tumbler lock system. The puzzle involves determining which keys can open which locks based on their column heights.

## Part 1

We need to analyze schematics that represent locks and keys as columns of various heights. The key characteristics are:

- **Locks**: Have the top row filled with `#` and bottom row empty with `.`
- **Keys**: Have the top row empty with `.` and bottom row filled with `#`
- Each schematic can be converted to a list of heights, one per column
- A key fits a lock if the sum of their heights in each column doesn't exceed the available space (6 units total)

The goal is to count how many unique lock/key pairs are compatible.

### Algorithm Analysis

The solution uses a straightforward brute-force approach:

1. **Parsing**: The input is split into individual grid schematics, then each grid is analyzed:
   - If the top row is all filled (`#`), it's classified as a lock
   - Otherwise, it's classified as a key
   - For each grid, count the height of filled cells in each column (subtracting 1 to account for the base)

2. **Compatibility Check**: The `no_overlap()` function checks if a key fits a lock:
   - For each column position, sum the heights from both the key and lock
   - Ensure no column exceeds the maximum height of 6 units
   - Return `True` if all columns are within bounds

3. **Counting**: Test every possible lock/key combination and count compatible pairs.

The time complexity is O(n × m × c) where n is the number of locks, m is the number of keys, and c is the number of columns (5 in this case).

### Key Insights

- The problem is essentially about ensuring no "collision" between key pins and lock tumblers
- The height constraint (6 units) represents the physical space available in the lock mechanism
- This is a classic constraint satisfaction problem solved with exhaustive search

## Part 2

Both parts of this puzzle are complete, providing two gold stars as the final day of Advent of Code 2024!

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1200px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday25.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
