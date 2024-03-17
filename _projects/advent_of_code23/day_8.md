---
title: "Day 8: Haunted Wasteland"
description: Graph Theory, No Pathfinding <br/> Difficulty ★★
layout: nested
---

# Day 8: Haunted Wasteland

[**link**](https://adventofcode.com/2023/day/8)

[**input**](https://adventofcode.com/2023/day/8/input)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/days/day8.py)

## Description

This problem defines a list of instructions and nodes. The nodes are each named with a three-character string and each node has two children, left and right, creating a graph structure.

The list of instructions are a series of individual left or right instructions, deciding the next node to visit. The instructions never terminate, but instead cycle continuously. The traversal through the graph terminates at node 'ZZZ'.

This is a graph problem following a pre-defined path.

## Part 1

Part 1 requires us to traverse the graph starting from 'AAA' until we terminate, and then return the number of instructions required to reach it.

In my solution, it seemed natural to represent the map as a directed graph with each vertex connected to two other vertices. From here, the answer can be found by iteration; We move through the graph until an 'ending node' is reached while keeping a counter for the number of instructions used.

## Part 2

In part 2, we are instead told to reinterpret which nodes are entry nodes and exit nodes. Nodes are entry nodes if they end in 'A', and exit nodes if they end in 'Z'. We now have multiple entrance and exit nodes. The entry nodes are traversed in the same manner as part 1, albeit simultaneously until all current nodes are exit nodes. We must then return the number of steps it took to end the sequence.

This problem is now far too large to brute force, and we must find another more numerical way to solve it. 

I found my solution by moving simulataneously through the graph, counting the number of steps for each entry point to reach an exit, until all routes being processed had reached an ending node at least once.

From here, the answer can be found by calculating the product of the prime factors of the number of steps for each starting node to reach *AN* ending.

## Improvements


### Algorithms

I represented the problem as a directed graph. Because the instructions are hard-coded, no decision have to be made. Therefore, there is no use for a depth-first search or breadth-first search algorithm.

### Software Engineering

I reused code through a base class 'NodesBase'.

Overall, I do not particular like my code structure to solve this problem for the following reasons:

 - The Node class that is used to represent the graph is bloated, it has too many attributes. For example, it contains `starting_node` and `ending_node` bools. The responsibility of interpreting a node as a starting or exit node should not be within the node class, but instead in the class that handles the complete graph structure.
 - I have separate classes for computing the answers to each part. These classes mainly store the same state, only differing in the `starting_node` and `ending_node` attributes within the Nodes.
 - `SimultaneousNodes` could reuse code for part 1, but it doesn't.
 - `NodesBase` should be an abstract base class.

Overall, it is not very good code. Although it produces the correct answer, it could be written in a much nicer way that is easier to understand, more maintainable, and has a simpler interface to users.
