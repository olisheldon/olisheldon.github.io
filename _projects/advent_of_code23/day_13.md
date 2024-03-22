---
title: "Day 13: Point of Incidence"
description: Recursion <br/> Difficulty ★★
layout: nested
---

# Day 13: Point of Incidence

[**link**](https://adventofcode.com/2023/day/13)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day13.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day13.py)

## Description

In this problem we consider a number of patterns. These patterns are 2D lists containing two types of element: ash ('.') and rock ('#'). Within these patterns are a number of horizontal and vertical lines create valid reflecting boundaries.

For the problem, we must find these horizontal (row-wise) and vertical (column-wise) boundary indices, and sum `100 * row_index + column_index` for each pattern. 

## Part 1

There are no fancy algorithms that I am aware of for this, only brute force iteration through every possible reflection boundary and checking if it is valid.

For part 1, the predicate for finding the reflection boundary is to perform a reflection and check that the two patterns are equal.

## Part 2

For part 2, the problem is made more complex: Upon closer inspection, we discover that every mirror has exactly one smudge, one piece of ash or rock that should be the opposite type.

In each pattern, we need to locate and fix the smudge that causes a different reflection line to be valid. (The old reflection line won't necessarily continue being valid after the smudge is fixed.)

Immediately, I began thinking this would require iterating over all possible patterns and looking for which one causes this condition to be true, but a more subtle and efficient algorithm is possible:

Instead of looking for a reflection boundary that results in a valid reflection, we instead looking for a reflection boundary such that the *reflection is incorrect by exactly one*. This is a much simpler problem that iterating over all possible patterns.

In fact, the only change required from part 1 is to change the final predicate for finding a _valid_ reflection boundary from no errors to exactly one error.

<!-- ## Improvements

### Part 1

### Part 2 -->

### Algorithms

Simple brute force. I am not aware of any efficient algorithms for this type of problem.

### Software Engineering

The logic for checking rowwise and columnwise is identical, only requiring a tranpose on the input matrix to switch between each. This increases code reuse in my solution.

The code for parts 1 and 2 is also reused. This was achieved by passing a predicate to the method that checks whether a reflection boundary produces a 'valid' reflection. This works as it is only the definition of a valid boundary that changes between part 1 and 2.

I would consider changing the interface to my `Pattern` class so that instead of having `smudge: bool` as an argument, a function could be passed directly that would determine a 'valid' reflection. This would make the code much more general. But, I think for this problem, the way I have written it is adequate.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday13.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>