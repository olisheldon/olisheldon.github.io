---
title: "Day 24: Crossed Wires"
description: Logic Gates and Debugging Swapped Wires <br/> Difficulty ★★★
layout: nested
---

# Day 24: Crossed Wires

[**link**](https://adventofcode.com/2024/day/24)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day24.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day24.py)

## Description

In this problem, we're given a system of boolean logic gates (AND, OR, XOR) with wire connections. We need to determine the decimal number produced by combining bits on all wires starting with 'z' in part 1, and then identify eight wires involved in swaps to fix the faulty system in part 2.

## Part 1

For part 1, we need to simulate the gate propagation system and determine the final value on each wire. The approach involves:

1. Creating a directed graph where each node is a wire and edges represent gate operations
2. Performing a depth-first search (DFS) to propagate values from input wires to output wires
3. Applying the appropriate boolean logic (AND, OR, XOR) based on the gate type
4. Reading the final values on all 'z' wires to form a binary number, which we convert to decimal

The simulation respects the constraint that gates must wait for both inputs before producing output.

The key to solving this part is maintaining a clear representation of the circuit as a graph and ensuring the propagation follows the correct rules. The `Node` class in the solution provides an abstraction for each wire, storing its connections and gate type.

## Part 2

Part 2 reveals that the system is actually meant to be a binary adder, where 'x' wires and 'y' wires represent two binary numbers, and 'z' wires should produce their sum. However, four pairs of gates have their output wires swapped.

The approach to solving this involves:

1. Verifying the structure of a proper binary adder (XOR gates for sum bits, propagation of carry bits)
2. Implementing verification functions to check if each bit position follows the correct adder pattern
3. Using a greedy algorithm to find pairs of nodes that, when swapped, improve the number of correctly functioning bit positions
4. Repeating the process four times to identify all four pairs of swapped wires

The challenge here is understanding how a binary adder should work and developing a strategy to identify which wires are swapped. The solution uses pattern matching against the expected structure of a binary adder and systematically tests potential swaps to find the correct ones.

## Improvements

### Algorithms

The solution uses a depth-first search for propagating values through the circuit, which is appropriate for a directed acyclic graph of logic gates. The verification functions for part 2 rely on pattern matching against the expected structure of a binary adder.

An alternative approach could use topological sorting to process nodes in dependency order, which would avoid redundant computations in the DFS. This would be especially beneficial for larger circuits with more complex dependencies.

For identifying the swapped wires, the current greedy approach works well but could potentially miss the optimal solution in more complex scenarios. A more comprehensive approach might involve using constraint satisfaction techniques to explore the space of possible swaps more thoroughly.

### Software Engineering

The code is well-structured with a clear separation between:
- Parsing and node creation
- Circuit simulation (part 1)
- Structure verification and swapped wire identification (part 2)

The `Node` class provides a clean abstraction for wires and their connections, which makes the code more maintainable and easier to understand.

Some potential improvements could include:
- Adding more comprehensive error handling for edge cases
- Implementing unit tests for each component
- Enhancing documentation with examples of different gate configurations
- Optimizing the swap identification algorithm to reduce the search space

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday24.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday24.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
