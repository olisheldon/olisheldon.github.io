---
title: "Day 8: Resonant Collinearity"
description: 2D Geometry, Line Intersections <br/> Difficulty ★★★
layout: nested
---

# Day 8: Resonant Collinearity

[**link**](https://adventofcode.com/2024/day/8)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day8.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day8.py)

## Description

This problem involves analyzing a grid of antennas and finding points where their signals create "antinodes". Each antenna is represented by a character (lowercase letter, uppercase letter, or digit) indicating its frequency. We need to find points where antennas of the same frequency align to create resonant effects.

The grid structure represents a map of antennas, and we must calculate how many unique locations contain antinodes based on specific resonance rules.

## Part 1

In Part 1, antinodes occur at points that are perfectly in line with two antennas of the same frequency, but only when one antenna is twice as far away as the other. For any pair of antennas with the same frequency, there are two antinodes, one on either side.

The solution involves:
1. Parsing the grid and grouping antennas by their frequency
2. For each pair of same-frequency antennas:
   - Calculate their relative positions
   - Determine the two antinode locations (one twice the distance in each direction)
3. Filtering out antinodes that fall outside the grid bounds
4. Counting unique antinode locations

## Part 2

Part 2 changes the rules of resonance - now an antinode occurs at any grid position exactly in line with at least two antennas of the same frequency, regardless of distance. Additionally, antennas themselves can be antinodes if they're in line with another antenna of the same frequency.

The solution approach changes to:
1. For each pair of same-frequency antennas:
   - Calculate all grid points that lie on the line through both antennas
   - Include the antenna positions themselves as antinodes
2. Filter points to stay within grid bounds
3. Count unique locations

## Improvements

### Algorithms

The solution uses vector arithmetic to calculate points along lines between antennas. 

#### Positive

- Clean separation between Part 1 and Part 2 logic
- Efficient use of sets to track unique antinode locations
- Vector-based approach makes the geometry calculations clear
- Good use of lambda functions for bounds checking

#### Negative

- Could extract common code between Part 1 and Part 2 into helper functions
- The `print_antinodes` function isn't used in the final solution
- Could benefit from more type hints and documentation
- Might be more efficient to pre-calculate grid bounds once

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday8.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday8.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>