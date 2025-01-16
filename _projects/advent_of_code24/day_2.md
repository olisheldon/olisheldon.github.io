---
title: "Day 2: Red-Nosed Reports"
description: Sequence validation <br/> Difficulty ★★
layout: nested
---

# Day 2: Red-Nosed Reports

[**link**](https://adventofcode.com/2024/day/2)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day2.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day2.py)

## Description

This problem involves analyzing safety reports from a Red-Nosed reactor. Each report contains a sequence of levels that need to follow specific safety rules.

## Part 1

For a report to be considered safe, it must satisfy two conditions:
1. The levels must be either strictly increasing or strictly decreasing
2. Adjacent levels must differ by at least 1 and at most 3

The solution uses Python's list comprehension and `zip` function to elegantly check these conditions:
- `zip(report, report[1:])` creates pairs of adjacent values
- `all(x < y for x, y in ...)` checks if all pairs are increasing
- `all(x > y for x, y in ...)` checks if all pairs are decreasing
- `all(1 <= abs(x - y) <= 3 for x, y in ...)` verifies the difference constraints

## Part 2

Part 2 introduces a "Problem Dampener" that can ignore one level in an otherwise unsafe report. This transforms the problem into checking if removing any single value from the sequence could make it safe.

The solution uses nested generators to efficiently:
1. Generate all possible modified reports by removing one value at a time
2. Check if any of these modified reports are safe
3. Count the total number of reports that are either naturally safe or can be made safe

## Improvements

### Algorithms

The current solution has a time complexity of:
- Part 1: O(n*m) where n is number of reports and m is length of each report
- Part 2: O(n*m²) due to checking each possible removal

Potential improvements:
- For Part 2, we could optimize by early stopping when we find the first valid modification
- We could cache common subsequences that are known to be safe/unsafe

### Software Engineering

The solution demonstrates good use of Python's functional programming features:
- Generator expressions to avoid storing intermediate results
- The `zip` function for pairwise iteration
- List comprehensions for concise data transformation

The `safe()` function is well-designed as it:
- Has a single responsibility (checking if a report is safe)
- Is pure (same input always produces same output)
- Is reusable between both parts

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday2.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
