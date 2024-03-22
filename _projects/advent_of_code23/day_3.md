---
title: "Day 3: Gear Ratios"
description: Grid parsing <br/> Difficulty ★
layout: nested
---

# Day 3: Gear Ratios

[**link**](https://adventofcode.com/2023/day/3)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day3.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day3.py)

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

This engine schematic is interpreted as follows:

 - Part numbers are adjacent (including diagonally) to at least one symbol (not including full stop).

## Part 1

Return the sum of all part numbers in a given engine schematic.

To do this, I parsed all of the numbers and symbols and into two separate containers that held their values and coordinates. I then performed checks on the boundary of all numbers to check for the presence of gears within this boundary.

## Part 2

In part 2 the concept of a gear is introduced with a more strict definition: any '*' symbol that is adjacent to exactly two part numbers. Each gear has a gear ratio that can be calculated from the multiplication of its two adjacent numbers. Return the sum of all gear ratios.

To complete this I used the same method as part 1, but with the stricter definitions of a gear to filter the symbols into only gears. From here, the gear ratios can be calculated, summed and returned.

## Improvements

### Algorithms

The time complexity of my solution is linear `O(N)` where N is the number of characters in the engine schematic. This assumes that the length of numbers within the engine schematic is much smaller than the width of the engine schematic, which seems reasonable.

### Software Engineering

The part_1() and part_2() methods contain too much logic. These should be pulled out into an 'Engine Schematic' class. However, the problem is not complex enough to warrant this.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday3.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>