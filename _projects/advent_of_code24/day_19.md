---
title: "Day 19: Linen Layout"
description: Dynamic Programming <br/> Difficulty ★★★
layout: nested
---

# Day 19: Linen Layout

[**link**](https://adventofcode.com/2024/day/19)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day19.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day19.py)

## Description

The problem presents us with a pattern matching challenge in an onsen (hot spring) setting. We need to determine whether certain towel patterns can be created using a given set of towel segments, and in part 2, count how many different ways we can arrange these segments to create each pattern.

Each towel pattern is made up of colored stripes (white (w), blue (u), black (b), red (r), or green (g)). We have a list of available towel segments (patterns) and need to check if longer target patterns can be created by combining these segments.

## Part 1

For part 1, we need to determine which target patterns can be created using the available towel segments. A pattern is possible if it can be constructed by concatenating one or more of the available segments. The segments cannot be reversed or modified.

The solution uses dynamic programming with a boolean array to track whether each prefix of the target pattern can be constructed. The approach is:

1. For each target pattern:
   - Create a boolean array `res` of length n+1 (where n is target length)
   - Set `res[-1] = True` (empty string is always possible)
   - Work backwards from end to start of target
   - For each position i and each available towel segment:
     - If segment matches at position i and remainder is possible, mark position i as possible
   - Final result is whether position 0 is possible

This approach effectively builds up from smaller subproblems to solve the larger problem of whether the entire pattern is possible.

## Part 2

Part 2 extends the problem to count all possible ways to construct each target pattern using the available segments. Instead of just determining if a pattern is possible, we need to count all valid combinations.

The solution modifies the part 1 approach to use counting instead of boolean values:

1. For each target pattern:
   - Create an integer array `res` of length n+1
   - Set `res[-1] = 1` (one way to make empty string)
   - Work backwards from end to start of target
   - For each position i and each available towel segment:
     - If segment matches at position i, add number of ways to make remainder to position i
   - Final result is number of ways to make entire pattern (position 0)

This dynamic programming approach efficiently computes all possible combinations without generating them explicitly.

## Improvements

### Algorithm

The current solution has a time complexity of O(N*M*K) where:
- N is number of target patterns
- M is average length of target patterns
- K is number of available segments

Possible improvements could include:
1. Preprocessing the available segments into a trie for faster matching
2. Memoizing results across similar patterns
3. Using pattern-matching algorithms for faster segment matching

### Software Engineering

The current solution could be improved by:
1. Adding type hints for better code clarity
2. Extracting the DP logic into a separate class
3. Adding comprehensive testing
4. Improving error handling for invalid inputs
5. Adding logging for debugging large inputs

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday19.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>