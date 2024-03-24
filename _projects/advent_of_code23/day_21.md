---
title: "Day 21: Step Counter"
description: Graph Flooding <br/> Difficulty ★★★
layout: nested
---

# Day 21: Step Counter

[**link**](https://adventofcode.com/2023/day/21)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day21.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day21.py)

## Description

In this problem we are given a map of a garden containing garden plots, rocks, and a starting position. Each step from the starting position can be in any of the cardinal directions onto adjacent garden plots.

## Part 1

For this part, we start from the starting position and count the number of tiles that it is possible to be standing on after taking 64 steps.

I completed this in a very convoluted way and inefficient way. I created a map mimicing the input map, but with extra state attached to each tile that stored whether that tile was reachable. Then, with each step/iteration, I iterated through every position on the map and updated its neighbours according to the rules.

This algorithm contains much repeated work, as discussed later.

## Part 2

For part 2, the map we are given now repeats indefinitely in all directions. Find how many garden plots the Elf could reach in exactly 26501365 steps.

I can not think of how to approach completing this problem. This number of steps is infeasible to iterate through for an indefinitely repeating map as it would use far too much memory. This makes me think that manual analysis would be the only potential approach to finding the solution.

## Improvements

### Part 1

My solution to part 1 is very inefficient, as this problem could instead be solved by a breadth-first fill.

If we reach a position with an even number of steps remaining, we can end up on that position again because we can just keep moving back and forth between that position and the position we just came from. This means that we never need to revisit the same space twice. If we get arrive at a garden plot and it is an odd number of steps from the start, that can never change. This means that once we have determined a position as reachable within the n steps, it will always remain reachable within greater than n steps.

### Part 2

### Algorithms

My approach has an exponential time complexity. This is because for every step we increase the number of steps we consider for the next step exponentially. Breadth-first fill would have an improved time complexity.

#### Breadth-First Fill

Breadth-first fill is possible because

 - If we reach a position in an **even** number of steps, we can end on that position by moving back and forth between the position and the position we just moved from.
 - If we reach a position in an **odd** number of steps, we can always *just* return to the start.

This means that we never need to reconsider positions we have already processed. This allows for the use of a breadth-first fill for this problem. I did not do this, and my confusion over how to approach part 2  would not be solved by changing this implementation detail. 

### Software Engineering

My approach had the tiles of the grid store state about whether they were reachable in the given number of steps. I do not like this approach as the grid stores state that it should not have responsibility for.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday21.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>