---
title: "Day 18: RAM Run"
description: Pathfinding, Grid Search <br/> Difficulty ★★★
layout: nested
---

# Day 18: RAM Run

[**link**](https://adventofcode.com/2024/day/18)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day18.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day18.py)

## Description

In this problem, we find ourselves in a computer's memory space that's being corrupted by falling bytes. The memory space is represented as a grid where bytes fall into specific coordinates, making those positions corrupted and impassable. Starting from the top-left corner (0,0), we need to find a path to reach the exit at the bottom-right corner (70,70) while avoiding corrupted memory locations.

## Part 1

The first part requires finding the shortest path from start to exit after 1024 bytes have corrupted various memory locations. This is a classic pathfinding problem with obstacles.

My solution uses Dijkstra's algorithm implemented with a priority queue (min heap) to find the shortest path. The key components are:

### Grid Creation
The solution first creates a grid representing the memory space, marking corrupted locations with '#' and safe locations with '.'. The corrupted locations are determined by the input coordinates of falling bytes.

### Pathfinding
Using Python's heapq module, the solution implements Dijkstra's algorithm to find the shortest path:
- The priority queue maintains a tuple of (steps, row, col)
- Each position can move in four directions (up, down, left, right)
- Invalid moves include:
  - Moving outside grid boundaries
  - Moving to already visited positions
  - Moving to corrupted memory locations ('#')

The time complexity is O(E log V) where E is the number of possible moves and V is the number of grid positions.

## Part 2

Part 2 asks for the coordinates of the first byte that will make the exit unreachable from the starting position. This is solved by incrementally simulating bytes falling and checking if a path to the exit still exists.

The solution uses the same pathfinding algorithm from Part 1 but calls it repeatedly with an increasing number of corrupted positions until no valid path exists. The last position that makes the path impossible is our answer.

## Improvements

### Algorithms

The current solution using Dijkstra's algorithm is efficient for the grid size we're working with. However, some potential improvements could be:

1. Using A* search instead of Dijkstra's, which could be faster by using a heuristic function (Manhattan distance to exit)
2. Implementing a bidirectional search from both start and end points

### Software Engineering

The code structure is clean and modular, but could be improved by:

1. Creating a MemoryGrid class to encapsulate grid operations
2. Adding type hints for better code documentation
3. Implementing a generic pathfinding interface that could support different algorithms

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday18.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday18.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>