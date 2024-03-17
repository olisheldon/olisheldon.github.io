---
title: "Day 3: Gear Ratios"
description: <br/> Grid parsing <br/> <br/> Difficulty ★
layout: nested
---

# Day 3: Gear Ratios

[**link**](https://adventofcode.com/2023/day/3)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day3.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/day3.py)

## Description

This problem requires analysing an 'engine schematic' (2D grid of digits, symbols, and full stops).

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

This engine schematic is interpret as follows:

 - Part numbers are adjacent (including diagonally) to at least one symbol (not including full stop).

## Part 1

Return the sum of all part numbers in a given engine schematic.

To do this, I parsed all of the numbers and into two separate containers and performed checks on the boundary of all numbers to check for gears.

## Part 2

We now define a gear as any '*' symbol that is adjacent to exactly two part numbers. Its gear ratio is the result of multiplying those two numbers together. Return the sum of all gear ratios.

The same method as part 1 was used with different conditions.

## Improvements

### Algorithms

The time complexity of my solution is linear O(N) where N is the number of characters in the engine schematic.

### Software Engineering

The part_1() and part_2() (outside of the problems classes) methods contain too much logic. These should be pulled out into an 'Engine Schematic' class. However, the problem is not complex enough to warrant this.