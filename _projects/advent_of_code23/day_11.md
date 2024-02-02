---
title: "Day 11: Cosmic Expansion"
description: L1 distance on 2D grid <br/> Difficulty ★
layout: nested
---

# Day 11: Cosmic Expansion

[**link**](https://adventofcode.com/2023/day/11)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day11.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day11.py)

## Description

This problem requires us to consider an image containing galaxies ('#') and empty space ('.'). Some rows and columns only contain empty space. For these rows and columns, the empty space has expanded by a factor of two. 

## Part 1

For part 1, we consider each pair of galaxies and calculate the distance between _including_ the expanded space. The answer we must return is the sum of these distances.

To do this, I preprocessed the image to recognise the columns and rows that should have the expansion coefficient applied. Then the problem is just a matter of iterating through each pair of galaxies, finding the columns and rows traversed in the L1 distance, and checking these columns and rows for being in the expanded rows or columns. From this, the sum of the distances can be returned.

## Part 2

Part 2 changes the problem to apply an expansion coefficient of 1000000 instead. The approach I used for part 1 can be easily modified to solve this.

## Improvements

### Part 1

My algorithm could be improved through the use of a cache/memoization. 

Consider:

```
......#     /  ......3
.......    /   .......
#..#...   /    1..2...
.......  /     .......
```

In calculating the distance between 1 and 3, if the distance between 2 and 3 is already known and stored we could solve the easier problem of calculating the distance between 1 and 2 and adding the distance from 2 to 3. It would be interesting to consider how this would affect the time complexity.

### Part 2

Part 2 does not make my solution any more complex, as the same number of operations are performed. The improvement suggested in part 1 improvements is also applicable to improving part 2.

### Algorithms

My solution has time complexity `O(N**2)`, but I believe this is ideal; The improvement suggested in part 1 would only improve the constants of this time complexity. This is because we are always going to have to consider all pairs of galaxies, which requires iterating through `(O(N))` galaxies for each galaxy `(O(N))`.

### Software Engineering

My solution to part 1 and part 2 use the same logic. This is a sign of a nicely written solution.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday11.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>