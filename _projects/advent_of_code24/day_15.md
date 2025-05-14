---
title: "Day 15: Warehouse Woes"
description: Grid Simulation <br/> Difficulty ★★
layout: nested
---

# Day 15: Warehouse Woes

[**link**](https://adventofcode.com/2024/day/15)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day15.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day15.py)

## Description

In this problem, we're dealing with a malfunctioning robot in a warehouse filled with boxes. The warehouse is represented as a grid where `#` represents walls, `O` represents boxes, `.` represents empty spaces, and `@` represents the robot.

The robot will attempt to execute a sequence of moves, and we need to predict how the boxes will shift around as the robot moves. The puzzle involves simulating these movements and calculating the final positions of all boxes.

## Part 1

In part 1, we simulate the robot's movement through the warehouse while tracking how it pushes boxes. The robot can move in four directions (up, down, left, right), and when it moves, it will push any boxes in its path until it reaches an empty space or a wall.

After completing all the robot's movements, we need to calculate the sum of all boxes' GPS coordinates. A box's GPS coordinate is calculated as 100 times its row position plus its column position.

The solution involves:
1. Parsing the grid and the robot's movement instructions
2. Finding the robot's initial position
3. For each move:
   - Determine the direction
   - Check what's in the path (boxes, empty spaces, or walls)
   - Push boxes as needed or cancel the move if impossible
   - Update the robot's position
4. Calculate the final sum of GPS coordinates for all boxes

## Part 2

In part 2, the warehouse layout is similar but everything except the robot is twice as wide. Specifically:
- Walls (`#`) become two wall characters (`##`)
- Boxes (`O`) become wide boxes represented as `[]`
- Empty spaces (`.`) become two empty spaces (`..`)
- The robot (`@`) remains the same size but is followed by an empty space (`@.`)

The movement logic becomes more complex as the wide boxes need to be treated as a single unit. When the robot pushes a wide box, both parts must move together.

The approach involves:
1. Widening the original grid according to the given rules
2. Adapting the movement logic to handle wide boxes
3. Calculating the GPS coordinates using the left side of each wide box

## Improvements

### Algorithm Efficiency

The solution uses a simulation approach where we directly manipulate the grid as we go. For part 2, I track all elements that need to move together using a "targets" list, which ensures wide boxes move as a single unit.

An alternative approach might have been to use a more abstract data structure to track positions rather than directly manipulating a grid, but the grid representation makes the problem more intuitive to solve and visualize.

### Edge Cases

One challenge was handling cases where boxes are pushed against walls or other boxes. The solution carefully checks if a move is valid by examining the entire path before committing to the move. For part 2, this becomes more complex as we need to check if all parts of a wide box can move without encountering obstacles.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:2200px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday15.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
