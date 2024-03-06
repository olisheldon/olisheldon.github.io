---
title: Day 8
description: NOT FINISHED. Why does this aDifficulty ★
layout: nested
---

# Day 8: Haunted Wasteland

[**link**](https://adventofcode.com/2023/day/8)

[**input**](https://adventofcode.com/2023/day/8/input)

[**code**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day8.py)

## Description

This problem defines a set of instructions and nodes. The nodes are each named with a three-character string and each node has two children, left and right.

The possible instructions are left or right, deciding the next node to visit. The instructions do not end, but instead loop continuously. The end of the traversal is a node named 'ZZZ'.

This is a graph problem, but simple as there is no pathfinding.

## Part 1

Part 1 requires us to traverse the nodes until 'ZZZ' is reached and return the number of instructions required to reach it.

In my solution, it seemed natural to represent the map as a directed graph with each vertex connected to two other vertices. From here, the answer can be brute-forced; Moving through the graph until an 'ending node' is reached.

## Part 2

In part 2, you instead interpret the nodes as input nodes if they end in 'A', and exit nodes if they end in 'Z'. The input nodes are traversed in the same manner as part 1, albeit simultaneously until all current nodes are exit nodes. We must then return the number of steps it takes to end the sequence.

This problem is now far too large to brute force, and we must think of other ways to solve it. My solution moves simulataneously through the graph until all routes being processed have reached an ending node once. The number of moves for each starting node to reach an end is stored.

From here, the number of steps required for all traversers to end up at an ending nodes simultaneously is the product of the prime factors of the number of steps for each starting node to reach AN ending.

## Improvements


### Algorithms

Representing problem as directed graph. Did not have to use depth-first search or breadth-first search.

### Software Engineering

I made nice use of code reuse through base class 'NodesBase'.
