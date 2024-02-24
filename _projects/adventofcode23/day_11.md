---
title: Day 11
description: INCOMPLETE
layout: nested
---

# Day 11: Cosmic Expansion

[link](https://adventofcode.com/2023/day/11)

[input](https://adventofcode.com/2023/day/11/input)

[code](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day11.py)

## Description

This problem requires us to consider an image containing galaxies ('#') and empty space ('.'). In rows and columns containing only empty space, each empty space for that row or column is two units of space instead of one. 

## Part 1

Consider each pair of galaxies, and calculate the distance between. Return the sum of these distances.

To do this, I preprocessed the image to recognise the colums and rows that should have the expansion coefficient applied. Then the problem is just a matter of iterating through each pair of galaxies, finding the columns and rows traversed in the L1 distance, and checking these columns and rows for being in the expanded rows or columns. From this, the sum of the distances can be returned.

## Part 2

Part 2 changes the problem to apply an expansion coefficient of 1000000 instead. The approach I used for part 1 can be easily modified to solve this.

## Improvements

### Part 1

The algorithm could be much improved through the use of a cache/memoization. 

Consider:

```
......#     /  ......3
.......    /   .......
#..#...   /    1..2...
.......  /     .......
```

In calculating the distance between 1 and 3, if the distance between 2 and 3 is already known and stored we could solve the easier problem of calculating the distance between 1 and 2 and adding the distance from 2 to 3. 

### Part 2

The improvement suggested above would speed up part too as well.

### Algorithms

### Software Engineering
