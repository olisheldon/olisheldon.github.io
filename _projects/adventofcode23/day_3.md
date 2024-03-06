---
title: Day 3
description: 2D symbol map interpreting
layout: nested
---

# Day 3: Gear Ratios

[**link**](https://adventofcode.com/2023/day/3)

## Description

This problem requires analysing an 'engine schematic' (2-D array of digits, symbols, and full stops).

```
467..114..
...*......
..35..633.
......#...
617*......
.....+.58.
..592.....
......755.
...$.*....
.664.598..
```

A number within this schematic is a part-number if it is adjacent (including diagonally) to a symbol.

## Part 1

Return the sum of all part numbers in a given engine schematic.

## Part 2

We now define a gear as any '*' symbol that is adjacent to exactly two part numbers. Its gear ratio is the result of multiplying those two numbers together.

Return the sum of all gear ratios.

## Improvements

### Algorithms

The time complexity of my solution is linear O(N) where N is the number of characters in the engine schematic.

### Software Engineering

the part_1() and part_2() methods contain too much logic. These should be pulled out into an 'Engine Schematic' class.