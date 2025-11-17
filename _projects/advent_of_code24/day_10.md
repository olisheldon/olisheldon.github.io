---
title: "Day 10: Hoof It"
description: Graph traversal with DFS <br/> Difficulty ★★
layout: nested
---

# Day 10: Hoof It

[**link**](https://adventofcode.com/2024/day/10)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day10.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day10.py)

## Description

In Day 10, we're given a topographic map represented as a grid of heights from 0-9. We need to analyze hiking trails that start at height 0 (trailheads) and end at height 9 (summits), where each step must increase height by exactly 1. Movement is allowed only in cardinal directions (up, down, left, right).

## Part 1

For part 1, we need to find the sum of scores for all trailheads, where a trailhead's score is the number of summit positions (height 9) that can be reached from that trailhead via valid hiking trails.

This is a graph traversal problem that can be solved using depth-first search (DFS). From each trailhead (height 0), we explore all possible paths that consistently increase in height by 1, keeping track of which summits we can reach. To avoid counting the same summit multiple times from a single trailhead, we mark summits as visited when we reach them.

## Part 2

Part 2 changes the scoring system - instead of counting reachable summits, we need to count the number of distinct possible paths from each trailhead to any summit. This is known as the trailhead's rating.

The core algorithm remains similar, but we modify our DFS to count paths rather than summits. When we reach a summit, instead of marking it visited, we count it as a valid path and continue backtracking to find other possible paths. The final result is the sum of all trailhead ratings.

## Solution

The solution uses a single DFS implementation that handles both parts through an enum-based scoring system:

```python
class Scoring(Enum):
    NUM_TRAILHEADS = auto()  # part 1
    NUM_DISTINCT_ROUTES = auto()  # part 2

def calc_trailhead_scores(scoring):
    grid = parse()
    ROWS, COLS = len(grid), len(grid[0])
    NEIGHBOURS = ((1, 0), (-1, 0), (0, 1), (0, -1))
    
    def dfs(r, c, prev):
        # Invalid conditions
        if (
            r not in range(ROWS) or
            c not in range(COLS) or
            (r, c) in visited or
            grid[r][c] - prev != 1
        ):
            return 0
        
        # Reached a summit
        if grid[r][c] == SUMMIT:
            if scoring == Scoring.NUM_TRAILHEADS:
                visited.add((r, c))
            return 1
        
        # Continue DFS
        res = 0
        visited.add((r, c))
        for dr, dc in NEIGHBOURS:
            res += dfs(r + dr, c + dc, grid[r][c])
        visited.remove((r, c))
        return res

    # Calculate total score across all trailheads
    res = 0
    for r in range(ROWS):
        for c in range(COLS):
            if grid[r][c] == TRAILHEAD:
                visited = set()
                res += dfs(r, c, TRAILHEAD - 1)
    return res
```

The key aspects of the solution are:

1. **DFS Implementation**: The recursive DFS function handles path exploration while enforcing the rules:
   - Must stay within grid bounds
   - Can't revisit positions
   - Must increase height by exactly 1
   - Returns count of valid paths/summits reached

2. **Visited Set Management**: We maintain a visited set to avoid cycles, but importantly:
   - Clear it for each new trailhead
   - Remove positions when backtracking to allow other paths to use them
   - For part 1, mark summits as visited to avoid counting them multiple times
   - For part 2, don't mark summits as visited to count all distinct paths

3. **Scoring System**: The enum-based scoring system allows the same core algorithm to handle both parts by slightly modifying the behavior at summit positions.

## Software Engineering

The solution demonstrates good software engineering practices:

1. **Code Organization**: Clear separation between parsing, logic, and main execution
2. **Enum Usage**: Using an enum for scoring types makes the code more maintainable and self-documenting
3. **Configurability**: Flexible file path handling for different input sources
4. **DRY Principle**: Single DFS implementation handles both parts
5. **Constants**: Clear naming of magic numbers (SUMMIT = 9, TRAILHEAD = 0)

The solution could be improved by:
1. Adding type hints
2. Breaking out the grid traversal logic into a separate class
3. Adding docstrings and more detailed comments
4. Including test cases for the example inputs

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday10.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday10.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
