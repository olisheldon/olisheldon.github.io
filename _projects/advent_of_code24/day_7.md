---
title: "Day 7: Bridge Repair"
description: Operator Permutations <br/> Difficulty ★★
layout: nested
---

# Day 7: Bridge Repair

[**link**](https://adventofcode.com/2024/day/7)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day7.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day7.py)

## Description

Help a group of engineers repair a rope bridge by solving their calibration equations. Each equation consists of a test value and a sequence of numbers. The challenge is to determine if the test value can be achieved by inserting operators between the numbers.

The operators are evaluated left-to-right (no precedence rules), and the numbers cannot be rearranged.

## Part 1

In Part 1, we need to identify which equations can be made true using only addition (+) and multiplication (*) operators. For each valid equation, we need its test value, and the final answer is the sum of all these test values.

The solution uses a depth-first search (DFS) approach to try all possible combinations of operators:

1. For each equation, we try to reach the target value by recursively:
   - Adding the next number
   - Multiplying by the next number

2. The DFS implementation includes optimization:
   - Early termination if current value exceeds target
   - Base case checks for reaching the end of numbers

## Part 2

Part 2 introduces a new concatenation operator (||) that combines digits (e.g., 12 || 345 = 12345). We need to find all equations that can be made true using any combination of +, *, and || operators.

The solution extends the Part 1 approach by:
1. Adding concatenation to the set of possible operators
2. Implementing concatenation using string manipulation

## Improvements

### Algorithms

The solution uses DFS which has time complexity O(2^n) for Part 1 and O(3^n) for Part 2, where n is the number of spaces between numbers in an equation. This is optimal as we need to try all possible operator combinations.

### Software Engineering

The code is concise and makes good use of Python's:
- Lambda functions for operator definitions
- Type hints for clarity
- Functional programming with `any()` for checking possible combinations

Potential improvements:
1. Could add more type hints, especially for the recursive function
2. Could split the parse function into smaller, more focused functions
3. Could add docstrings and comments explaining the DFS approach

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday7.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday7.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>