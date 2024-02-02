---
title: "Day 24: Never Tell Me The Odds"
description: Intersecting Lines <br/> Difficulty ★★★
layout: nested
---

# Day 24: Never Tell Me The Odds

[**link**](https://adventofcode.com/2023/day/24)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day24.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day24.py)

## Description

In this problem, we are provided with a snapshot a system of hailstones positions and velocities. Asssuming the hailstones move in a perfectly linear motion, we must count how many of the hailstones **paths** (not just collisions) will intersect within a test area.

## Part 1

For part 1, we only consider the X and Y axes.

The hailstones can be represented as lines. This means that they can be represented in the form

```
ax + by = c
```

Our first task is to convert each hailstone to this form, and then model our system as a system of lines and apply the correct algebraic formulae. Then, checking that:

 * There is a collision
 * The collision occurs in the test area
 * It does not happen in negative time (the past)

If all of these are true, these pair of hailstones should be counted.

## Part 2

For part 2, we are asked to find a position and velocity such that this new hailstone collides with every hailstone.

This problem could be solved in the same way as part 1, but with much more complex and involved algebra. 
<!-- Alternatively, a simultaneous-equation-solving library could be used. -->

## Improvements

### Part 1

My solution to part 1 is analytical and produces an optimal time complexity.

<!-- ### Part 2 -->

### Algorithms

Part 1 only requires basic algebra. Part 2 will require much more complex algebra.

<!-- ### Software Engineering -->


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday24.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>