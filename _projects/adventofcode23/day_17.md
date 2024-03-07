---
title: Day 17
description: INCOMPLETE
layout: nested
---

# Day 17: Cosmic Expansion

[**link**](https://adventofcode.com/2023/day/17)

[**input**](https://adventofcode.com/2023/day/17/input)

[**code**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day17.py)

## Description

This problem considers a 2D grid of integers. Each square within the grid represents the 'heat loss' accumulated by traversing through that tile. For all intents and purposes this can be more simply interpreted as the cost of travelling through the square, with the total cost of a path being the sum of the heat losses.

Our job is to find the path from the top-left square to the bottom-right square such that the heat loss accumulated is minimized. To make the problem more interesting, further constraints are placed on the shape of our path:

 - We can only move at most three squares in the same direction before we must turn left or right.
 - We can not move backwards, only continue in the same direction or in an orthogonal direction.

## Part 1

This is path finding through a grid, minmizing the cost of this path. This is a classic problem that can be easily solved with Dijkstra's Algorithm [**link**](). It is possible to use simple breadth-first search to solve, but it will take an unfeasibly long amount of time to solve.

Dijkstras Algorithm speeds up breadth-first search by replacing the queue of nodes to visit with a priority queue. This means that we will always look at the next node that is the most promising candidate for minimizing the cost. 

## Part 2

In part 2, the constraints placed on the shape of our path through the graph is changed:

 - A valid path must move a minimum of four tiles in the same direction before it can turn *or* before it can stop at the end.
 - A valid path must not move a more than ten consecutive blocks in the same direction.

This amounts to a change in considering whether the next state we are evaluating is valid. This can be done by changing the predicate we use for checking that a new path's state is valid.

## Improvements

### Part 1

Overall, I think the general time complexity is as good as it can get. The constants within the time complexity could be possibly improved by being more careful in the new directions we consider, but this would make a negligible difference.

### Part 2

### Algorithms

### Software Engineering

As the only difference between part 1 and 2 was the predicate used for determining if the new crucible state was valid, I added passing this predicate to the method contain Dijkstras Algorithm. The other choice was to hard code each implementation.

I prefer the runtime variation because it allows users to choose the predicate they want, and results in no repeated code within the graphs implementation.