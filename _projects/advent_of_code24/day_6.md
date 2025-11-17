---
title: "Day 6: Guard Gallivant"
description: Guard Patrol Simulation <br/> Difficulty ★★★
layout: nested
---

# Day 6: Guard Gallivant

[**link**](https://adventofcode.com/2024/day/6)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day6.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day6.py)

## Description

This problem involves simulating a guard's patrol route in a 2D grid. The guard follows a simple set of rules:
1. If there is an obstacle directly ahead, turn 90 degrees right
2. Otherwise, move forward one step

The input is a grid where '^' represents the guard's starting position (facing up), '#' represents obstacles, and '.' represents empty spaces.

## Part 1

Part 1 asks us to count how many distinct positions the guard visits before leaving the mapped area. This is a straightforward simulation problem that requires:

1. Finding the guard's initial position
2. Implementing the movement rules
3. Tracking visited positions
4. Detecting when the guard leaves the grid

The solution uses `itertools.cycle` to handle the rotation of directions elegantly, cycling through up, right, down, and left movements. A set is used to track visited positions efficiently.

## Part 2

Part 2 asks us to find how many different positions we could place a new obstacle that would cause the guard to get stuck in a loop. This builds on Part 1 by:

1. Finding all possible positions for the new obstacle (empty spaces)
2. For each position:
   - Temporarily placing an obstacle
   - Running the simulation to detect if it creates a loop
   - Removing the obstacle

The key insight is that a loop exists if we encounter the same state (position + direction) twice. We track states as tuples of (row, col, dr, dc) where (dr, dc) represents the current direction.

## Improvements

While the current solution is sufficient for the given input sizes, potential optimizations could include:

- Using a more efficient data structure for state tracking
- Parallelizing the obstacle placement simulations in Part 2
- Early termination of simulations that clearly won't result in loops

### Algorithms

The solution uses:
- Grid traversal with direction vectors
- State tracking using sets
- Cycle detection for Part 2

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday6.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday6.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>