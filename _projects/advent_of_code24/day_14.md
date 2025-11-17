---
title: "Day 14: Restroom Redoubt"
description: Robot collision prediction <br/> Difficulty ★★
layout: nested
---

# Day 14: Restroom Redoubt

[**link**](https://adventofcode.com/2024/day/14)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day14.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day14.py)

## Description

This problem involves predicting the movement of robots in a confined space. Each robot has a position (x,y) and velocity (vx,vy), and they move in straight lines. When a robot reaches the edge of the space, it teleports to the opposite side (wrapping around). The space is 101 tiles wide and 103 tiles tall.

The objective is to help a historian safely navigate to a bathroom by predicting where security robots will be in the future. These robots move in predictable straight lines but can teleport from one edge of the space to the opposite edge when they would otherwise hit a boundary.

## Part 1

For Part 1, we need to simulate 100 seconds of robot movement and determine a "safety factor" by counting robots in each quadrant and multiplying these counts together.

The solution is fairly straightforward:
1. Parse the input to get each robot's position and velocity
2. Simulate 100 seconds by updating each robot's position based on its velocity
3. Count robots in each quadrant (excluding those on the middle lines)
4. Multiply these counts to get the safety factor

The position update uses modulo arithmetic to handle the wrapping:
```python
pos[0] = (pos[0] + vel[0]) % ROWS
pos[1] = (pos[1] + vel[1]) % COLS
```

My approach simply implements this simulation directly, iterating through 100 time steps and updating all robot positions accordingly. The safety factor calculation excludes robots that are on the middle lines (horizontally or vertically) and multiplies the count of robots in each quadrant.

## Part 2

Part 2 asks for the fewest number of seconds that must elapse for the robots to display a Christmas tree pattern (the "Easter egg").

This part is more complex and requires detecting a specific pattern. The approach I took is:
1. For each possible time (up to ROWS*COLS), calculate robot positions
2. Calculate the safety factor for each time
3. Find the minimum non-zero safety factor, which corresponds to the Easter egg pattern

The key insight is that we don't need to actually simulate step by step - we can directly calculate positions for any given time t using:
```python
new_px = (px + vx * iteration) % ROWS
new_py = (py + vy * iteration) % COLS
```

This is possible because the movement is deterministic and linear. Since the position for any robot at any time can be calculated directly, we can efficiently check many different timestamps to find when the robots form the desired pattern.

The minimum non-zero safety factor corresponds to the time when robots arrange themselves in a Christmas tree pattern due to the problem's constraints.

## Improvements

### Part 1
The solution is already efficient for the requirements of the problem, but we could potentially optimize by calculating the final positions directly rather than simulating each step, similar to the approach used in part 2.

### Part 2
Instead of checking all possible times up to ROWS*COLS, we might be able to use mathematical properties to narrow down the search space. For instance, we could analyze the periods of individual robot movements to identify candidate times when they might align in a pattern.

There's also potential to improve the pattern detection algorithm. The current implementation uses a minimal safety factor as a proxy for detecting the Christmas tree pattern, but a more direct pattern recognition approach could be more reliable.

### Algorithms
The current approach is efficient with O(N) time complexity for Part 1 (where N is the number of robots) and O(N*T) for Part 2 (where T is the maximum time checked).

A potential improvement would be to use the Chinese Remainder Theorem to find cycles in the robot movements and calculate when they would align in specific patterns, which could reduce the search space significantly.

### Software Engineering
- The code could benefit from more comments explaining the approach
- The `detect_christmas` function could be improved with a clearer implementation
- Error handling for edge cases could be added
- The grid visualization functions could be enhanced to make debugging easier
- Constants and magic numbers could be better documented

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday14.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday14.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>