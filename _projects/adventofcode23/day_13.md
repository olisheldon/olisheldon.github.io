---
title: Day 13
description: INCOMPLETE
layout: nested
---

# Day 13: Point of Incidence

[link](https://adventofcode.com/2023/day/13)

[input](https://adventofcode.com/2023/day/13/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day13.py)

## Description

We are asked to consider a number of patterns. These patterns are 2D lists containing two types of element: ash and rock. Within these patterns are a number of horizontal and vertical lines that can be correctly interpreted as a reflecting boundary.

For the problem, we must find these horizontal (row-wise) and vertical (column-wise) boundary indices, and sum `100 * row_index + column_index` for each pattern. 

## Part 1

There are no fancy algorithms that I am aware of for this, only brute force iteration through every possible reflection boundary and checking if it is valid.

For part 1, the predicate for finding the reflection boundary is to perform a reflection and check that the two patterns are equal.

## Part 2

Upon closer inspection, you discover that every mirror has exactly one smudge: exactly one . or # should be the opposite type.

In each pattern, you'll need to locate and fix the smudge that causes a different reflection line to be valid. (The old reflection line won't necessarily continue being valid after the smudge is fixed.)

For part 2, we are told that each pattern has exactly one mistake in it. That means that for each pattern one piece of rock or ash needs to be swapped. We are told that the piece of ash or rock that needs to be swapped will cause another reflection line to be valid. 

Immediately, I began thinking this would require iterating over all possible patterns and looking for which one causes this condition to be true, but the actual method require is much simpler:

Instead of looking for a reflection boundary that results in a valid reflection, we are now looking for a reflection boundary such that the *reflection has exactly one issue*. This is a much simpler problem that iterating over all possible patterns.

In fact, the only change required from part 1 is to change the final predicate for finding a _valid_ reflection boundary.

## Improvements

### Part 1

### Part 2

### Algorithms

Simple brute force. I don't think there are any particular algorithms for this type of problem.

### Software Engineering

Reuse of code between parts one and two.