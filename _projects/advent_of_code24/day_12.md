---
title: "Day 12: Garden Groups"
description: Graph Analysis and Geometry <br/> Difficulty ★★
layout: nested
---

# Day 12: Garden Groups

[**link**](https://adventofcode.com/2024/day/12)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day12.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day12.py)

## Description

This problem involves analyzing plots of garden plants, where each letter represents a different type of plant. Plots with the same type of plant that are adjacent horizontally or vertically form a region. We need to calculate the cost of fencing around these regions based on their properties.

### Example

```
AAAA
BBCD
BBCC
EEEC
```

This arrangement has 5 distinct regions of plants (labeled A, B, C, D, and E).

## Part 1

For Part 1, we need to calculate the price of fencing by multiplying each region's area by its perimeter. The area is simply the number of plots in a region, while the perimeter is the number of sides of plots that don't touch another plot of the same plant type.

The solution employs a depth-first search (DFS) approach to identify regions and calculate their properties:

1. Parse the input grid of plant types
2. For each unvisited plot in the grid:
   - Run DFS to identify all connected plots of the same plant type
   - Calculate the region's perimeter and area during traversal
   - Store these values for later calculation
3. Calculate the total price by summing the product of each region's perimeter and area

The perimeter calculation needs careful consideration. For each plot in a region, we examine its four neighbors (up, down, left, right). If any neighbor is out of bounds or contains a different plant type, that side contributes to the perimeter.

### Implementation Details

The `calc_perimeter` function determines how many sides of a given plot contribute to the region's perimeter:

```python
def calc_perimeter(grid, r, c, veg):
    perimeter = 0
    for dr, dc in NEIGHBOURS:
        if r + dr not in range(ROWS) or c + dc not in range(COLS) or grid[r + dr][c + dc] != veg:
            perimeter += 1
    return perimeter
```

The DFS function traverses the region and accumulates the perimeter and area:

```python
def dfs(r, c, veg): # -> perim, area
    if (
        (r, c) in visited or
        r not in range(ROWS) or
        c not in range(COLS) or
        grid[r][c] != veg
        ):
        return 0, 0
    visited.add((r, c))
    
    perim = calc_perimeter(grid, r, c, veg)
    area = 1
    
    for dr, dc in NEIGHBOURS:
        res = dfs(r + dr, c + dc, veg)
        perim += res[0]
        area += res[1]
    return perim, area
```

## Part 2

In Part 2, the pricing formula changes. Instead of using the perimeter, we need to count the number of "sides" each region has, regardless of length. This is essentially calculating the number of "corners" that define the region's shape.

For this part, I switch to a BFS (breadth-first search) approach to identify regions:

1. Use BFS to find all regions as in Part 1
2. For each region, calculate the number of sides using a geometric approach:
   - Consider all potential corner points (half-coordinates between grid cells)
   - Analyze each corner's surrounding cells to determine if it contributes to the region's shape
   - Count corners based on specific patterns of occupied/unoccupied cells

The key insight is that by examining the half-integer coordinates between grid cells, we can identify the "corners" that define each region's shape. The number of sides can then be determined by analyzing the configuration of cells around each potential corner.

### Corner Counting Logic

The solution examines each potential corner point (the intersections between grid cells) and counts them based on the pattern of occupied cells:

```python
def count_sides(region):
    corner_candidates = set()
    for r, c in region:
        for cr, cc in [(r-0.5, c-0.5), (r+0.5, c-0.5), (r+0.5, c+0.5), (r-0.5, c+0.5)]:
            corner_candidates.add((cr, cc))
    
    corners = 0
    for cr, cc in corner_candidates:
        config = [
            (int(cr-0.5), int(cc-0.5)) in region,
            (int(cr+0.5), int(cc-0.5)) in region,
            (int(cr+0.5), int(cc+0.5)) in region,
            (int(cr-0.5), int(cc+0.5)) in region,
        ]
        
        number = sum(config)
        if number == 1:
            corners += 1
        elif number == 2:
            if (config[0] and config[2]) or (config[1] and config[3]):
                corners += 2
        elif number == 3:
            corners += 1
```

This elegantly handles all cases:
- A single occupied cell creates one corner
- Two diagonal occupied cells create two corners
- Three occupied cells create one corner
- Four occupied cells (fully enclosed) create no corners

## Improvements

The solution uses different approaches for Part 1 and Part 2, which might not be the most efficient in terms of code reuse. A unified approach could be implemented where both perimeter and side count are calculated in a single traversal.

Additionally, we could optimize memory usage by tracking visited cells within the grid itself instead of using a separate set, especially for large inputs.

### Software Engineering

The code is well-structured with separate functions for parsing input, solving each part, and helper functions for specific calculations. The use of both DFS and BFS demonstrates flexibility in approach based on the specific requirements of each part.

## Solution