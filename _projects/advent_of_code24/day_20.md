---
title: "Day 20: Race Condition"
description: Graph Search with Cheating <br/> Difficulty ★★★
layout: nested
---

# Day 20: Race Condition

[**link**](https://adventofcode.com/2024/day/20)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day20.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day20.py)

## Description

This problem presents an interesting twist on the classic pathfinding problem. We need to find paths through a maze-like racetrack, but with a unique mechanic: the ability to "cheat" by passing through walls for a limited number of moves.

### Key Components

The puzzle involves:
- A grid-based racetrack with walls (#), open track (.), start position (S), and end position (E)
- Movement in four directions (up, down, left, right), each taking 1 picosecond
- A cheating mechanic that allows passing through walls

### The Cheating Mechanic

#### Part 1
- Can cheat exactly once during the race
- Cheating can last up to 2 picoseconds
- Must end cheat on normal track (not in a wall)

#### Part 2
- Same rules but cheating can last up to 20 picoseconds
- Still can only cheat once
- Unused cheat time is lost

## Solution Approach

### Core Algorithm

The solution uses a combination of:
1. Dijkstra's algorithm for finding the shortest path without cheating
2. A coordinate-based approach for finding valid cheat positions

Key functions:

#### Default Path Finding
```python
def min_path(grid, start, end, cache):
    min_heap = [(0, start[0], start[1], [])]  # (steps, r, c, history)
    while min_heap:
        steps, r, c, history = heapq.heappop(min_heap)
        # Process current position and add neighbors
```

This function implements a standard shortest path algorithm using a priority queue, which ensures we always process the path with the fewest steps first.

#### Finding Cheat Possibilities
```python
def possible_coords(r, c, grid, cheat_distance):
    cheat_range = range(-cheat_distance, cheat_distance + 1)
    possible_coords = []
    for dr in cheat_range:
        for dc in cheat_range:
            # Check if coordinate is valid and reachable within cheat distance
```

This function finds all possible coordinates that could be reached by cheating from a given position, considering the maximum cheat distance allowed.

### Optimization Techniques

1. **Caching**: The solution caches default path lengths to avoid recalculating them:
```python
def all_min_path_no_cheat(grid, end):
    default_times = {}
    for r in range(ROWS):
        for c in range(COLS):
            if grid[r][c] in (TRACK, START):
                default_times[(r, c)] = min_path(grid, (r, c), end, dict())
```

2. **Early Termination**: The pathfinding algorithm stops when it finds the end position or when it reaches a previously cached position.

### Time Calculation

The solution calculates time savings by:
1. Finding the default time from start to end
2. For each possible cheat start/end combination:
   - Calculate time to cheat start
   - Add cheat duration
   - Add remaining time to end
   - Compare with default time to find savings

## Improvements

### Potential Optimizations

1. **Space Efficiency**: The current solution stores a complete cache of paths. This could be optimized to only store necessary paths.

2. **Pruning**: We could add more aggressive pruning of impossible cheat combinations based on Manhattan distance calculations.

### Alternative Approaches

An alternative approach could use:
1. A bidirectional search from both start and end
2. Pre-computation of "cheat zones" where cheating would be beneficial
3. Dynamic programming to build up optimal paths incrementally

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday20.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
