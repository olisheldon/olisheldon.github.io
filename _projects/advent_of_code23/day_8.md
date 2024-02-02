---
title: "Day 8: Haunted Wasteland"
description: Graph Theory, No Pathfinding <br/> Difficulty ★★
layout: nested
---

# Day 8: Haunted Wasteland

[**link**](https://adventofcode.com/2023/day/8)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day8.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day8.py)

## Description

This problem contains a list of instructions and nodes. Each node is labelled with a three-character string and has two children, left and right, creating a graph structure.

The list of instructions are a series of individual left or right instructions, deciding the next node to visit. The instructions never terminate, but instead cycle continuously. The traversal through the graph terminates at node 'ZZZ'.

This is a graph problem, with traversal via a pre-defined path.

## Part 1

Part 1 requires us to traverse the graph starting from 'AAA' until the terminating node is reached. The number of instructions required to terminate should be returned.

In my solution, it seemed natural to represent the map as a directed graph with each vertex connected to two other vertices. From here, the answer can be found by iteration; We move through the graph until an 'ending node' is reached while keeping a counter for the number of instructions used.

## Part 2

In part 2, we are instead told to reinterpret which nodes are entry nodes and exit nodes. Nodes are entry nodes if they end in 'A', and exit nodes if they end in 'Z'. We now have multiple entrance and exit nodes. The entry nodes are traversed in the same manner as part 1, albeit simultaneously and we only terminate the sequence once all current nodes are exit nodes. We must then return the number of steps it took to end the sequence.

This problem is now far too large to brute force, and we must consider numerical ways to solve it. 

I considered each entry node separately, tracking the *minimum number of instructions* it took for each entry node to reach its first ending node. Once all routes had been processed, I found the prime factors of each of these *minimum number of instructions*. The answer can then be found by taking the product over the unique prime factors.

## Improvements


### Algorithms

I represented the problem as a directed graph. Because the instructions are hard-coded, no decision have to be made. Therefore, there is no use for a depth-first search or breadth-first search algorithm.

#### Positive

 - I reused code through a base class 'NodesBase'.

#### Negative

 - The Node class that is used to represent the graph is bloated, it has too many attributes. For example, it contains `starting_node` and `ending_node` bools. The responsibility of interpreting a node as a starting or exit node should not be handled by the node class, but instead by the class that handles the complete graph structure (in my case `Nodes` and `SimultaneousNodes`).
 - I have separate classes for computing the answers to each part. These classes mainly store the same state, only differing in the `starting_node` and `ending_node` attributes within the Nodes.
 - `SimultaneousNodes` could reuse code for part 1, but it doesn't.
 - `NodesBase` should be an abstract base class. There should never be a need to instantiate this class.

Overall, it is not very good code. Although it produces the correct answer, it could be written in a much nicer way that is easier to understand, more maintainable, and has a simpler interface for users.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday8.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>