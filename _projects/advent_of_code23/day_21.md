---
title: "Day 21: Step Counter"
description: <br/> Flooding graph <br/> <br/> Difficulty ★★★
layout: nested
---

# Day 21: Step Counter

[**link**](https://adventofcode.com/2023/day/21)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day21.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/day21.py)

## Description

In this problem we are given a map of a garden containing garden plots, rocks, and a starting position (that is a garden plot). Each step from the starting position can be in any of the cardinal directions.

## Part 1

Starting from the starting position, count the number of tiles it is possible to be standing in after taking 64 steps.

I completed this in a very convoluted way and inefficient way. I created a map mimicing the input map, but with extra state attached to each tile that stored whether that tile was reachable. Then, with each step/iteration I iterated through every position on the map and updated its neighbours according to the rules.

## Part 2

For part 2, the map we are given now repeats indefinitely in all directions. Find how many garden plots the Elf could reach in exactly 26501365 steps.

I can not think of how to complete this problem.

## Improvements

### Part 1

My solution to part 1 is very inefficient, as this problem could instead be solved by a breadth-first fill. This is possible because 

If we reach a position with an even number of steps remaining, we can end up on that position because we can just keep alternating back and forth between that position and another position. Therefore, we never need to revisit the same space twice. If we get to it, if its on an odd number of steps, that can never changes. If on an even number of steps we can always return to S with zero steps remaining.

### Part 2

### Algorithms

I used a silly approach with `O(blah)` time complexity. Breadth-first fill has a `O(blah blah)` time complexity.

### Software Engineering