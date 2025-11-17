---
title: "Day 16: Reindeer Maze"
description: Maze pathfinding with Dijkstra's algorithm <br/> Difficulty ★★★
layout: nested
---

# Day 16: Reindeer Maze

[**link**](https://adventofcode.com/2024/day/16)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day16.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day16.py)

## Description

This problem involves finding optimal paths through a maze where movement has different costs. A reindeer starts at position 'S' facing East and needs to reach position 'E'. Moving forward costs 1 point, while rotating 90 degrees (clockwise or counterclockwise) costs 1000 points. The challenge is to find the path with the lowest total score.

## Part 1

Find the lowest score a reindeer could possibly get when navigating from start to end.

I solved this using Dijkstra's algorithm with a priority queue (min-heap). The state space includes both position (row, column) and direction, since turning has a significant cost. Each state in the queue contains:
- Current score
- Position (row, column) 
- Direction (North, East, South, West)
- History for visualization

From each state, three moves are possible:
- **Move forward**: Add 1 to score and advance one tile in current direction
- **Turn clockwise**: Add 1000 to score, stay in same position, rotate direction
- **Turn counterclockwise**: Add 1000 to score, stay in same position, rotate direction

The algorithm uses a visited set to avoid processing the same (position, direction) state multiple times. When the end tile is reached, the current score is the optimal solution.

## Part 2

Find how many tiles are part of at least one optimal path through the maze.

This extends Part 1 by tracking all optimal paths, not just finding the minimum cost. The approach uses:

1. **Modified Dijkstra's**: Instead of stopping at the first solution, continue processing until all states with the optimal cost are found
2. **Backtracking**: Maintain a backtrack dictionary that maps each state to all previous states that could lead to it with optimal cost
3. **State reconstruction**: Starting from all end states with optimal cost, work backwards through the backtrack dictionary to find all states that participate in optimal paths

Key improvements over Part 1:
- Track multiple paths to the same state if they have equal cost
- Use backtracking to reconstruct all optimal paths
- Count unique tile positions (ignoring direction) that appear in any optimal path

The algorithm ensures that when multiple paths reach the same state with equal cost, all previous states are preserved for backtracking.

## Improvements

### Algorithm Choice

Using Dijkstra's algorithm is optimal for this problem because:
- Edge weights are non-negative (1 for movement, 1000 for rotation)
- We need the shortest path in a weighted graph
- The state space (position + direction) is manageable

### State Representation

The solution represents direction as integers (0-3) mapping to North, East, South, West. This allows efficient rotation using modular arithmetic:
- Clockwise: `(direction + 1) % 4`
- Counterclockwise: `(direction - 1) % 4`

Direction vectors are stored in a ROTATIONS tuple for easy coordinate updates.

### Part 2 Optimization

The backtracking approach efficiently finds all optimal paths without exponential enumeration. By working backwards from end states, we only consider states that actually contribute to optimal solutions.

### Software Engineering

The code uses clear separation between parts 1 and 2, with Part 2 being a natural extension that adds backtracking logic. The visualization functions help debug and understand the solution paths.

The direction handling could be simplified by using complex numbers or 2D vectors, but the current enum-based approach provides clear semantics and easy rotation operations.

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:2500px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday16.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday16.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
