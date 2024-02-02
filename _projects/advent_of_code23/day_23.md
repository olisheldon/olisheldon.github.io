---
title: "Day 23: A Long Walk"
description: DAG / Graph Traversal <br/> Difficulty ★★★
layout: nested
---

# Day 23: A Long Walk

[**link**](https://adventofcode.com/2023/day/23)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day23.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day23.py)

## Description

Day 23 presents a hike through a 2D grid representing hiking trails through a forest. We start at the top-left of the grid, and exit at the bottom-right. Some of the path tiles through the forest are sloped, such that they can only be traversed in one direction (the traversable direction is shown through the orientation of a '>' symbol).

### Test Case Example

```
#.#####################          #S#####################
#.......#########...###          #OOOOOOO#########...###
#######.#########.#.###          #######O#########.#.###
###.....#.>.>.###.#.###          ###OOOOO#OOO>.###.#.###
###v#####.#v#.###.#.###          ###O#####O#O#.###.#.###
###.>...#.#.#.....#...#          ###OOOOO#O#O#.....#...#
###v###.#.#.#########.#          ###v###O#O#O#########.#
###...#.#.#.......#...#          ###...#O#O#OOOOOOO#...#
#####.#.#.#######.#.###          #####.#O#O#######O#.###
#.....#.#.#.......#...#          #.....#O#O#OOOOOOO#...#
#.#####.#.#.#########v#          #.#####O#O#O#########v#
#.#...#...#...###...>.#    ->    #.#...#OOO#OOO###OOOOO#
#.#.#v#######v###.###v#          #.#.#v#######O###O###O#
#...#.>.#...>.>.#.###.#          #...#.>.#...>OOO#O###O#
#####v#.#.###v#.#.###.#          #####v#.#.###v#O#O###O#
#.....#...#...#.#.#...#          #.....#...#...#O#O#OOO#
#.#########.###.#.#.###          #.#########.###O#O#O###
#...###...#...#...#.###          #...###...#...#OOO#O###
###.###.#.###v#####v###          ###.###.#.###v#####O###
#...#...#.#.>.>.#.>.###          #...#...#.#.>.>.#.>O###
#.###.###.#.###.#.#v###          #.###.###.#.###.#.#O###
#.....###...###...#...#          #.....###...###...#OOO#
#####################.#          #####################O#
```


### Longest Path

Unlike shortest path, there is no efficient algorithm for finding the longest path. This makes any optimization to our graph representation very important. 

## Part 1

For part 1, we are asked to find the optimal path from the start to the exit under the constraint of having the most scenic hike (longest path while never stepping on the same tile twice). This means finding the longest traversal through the graph without any cycles.

A noteworthy feature of our grid is that all paths are only one tile wide. As we can not go back on ourselves due to our *scenic hike constraint*, many of the tiles require no decisions so should not be considered in our longest-path algorithm. Therefore this problem can be simplified enormously by performing edge contraction.

### Edge Contraction

In edge contraction, we ignore edges on our graph that require no decision thereby decreasing the size of the graph. 

If we take a subgrid from our example, we can see how edge contraction can be used to create an adjacency list that perfectly captures the graph in a much more concise way:

```
#.#######    #1#######
#.......#    #.......#
#######.#    #######.#
###.....#    ###.....#
###v#####    ###v#####           
###.>...#    ###2>...#           -->- ...
###v###.#    ###v###.#          /  
###...#.# -> ###...#.# -> 1 ->- 2       ...
#####.#.#    #####.#.#          \      /
#.....#.#    #.....#.#           -->- 3
#.#####.#    #.#####.#                 \
#.#...#..    #.#...#..                  ...
#.#.#v###    #.#.#v###
#...#.>.#    #...#3>.#
#####v#.#    #####v#4#
```

In my code, this adjacency list is stored as nested dictionaries

```python
dict(Coord(i=0, j=1): {Coord(i=5, j=3) : 15},
     Coord(i=5, j=3) : {Coord(i=13, j=5): 22},
     Coord(i=13, j=5): {Coord(i=14, j=7): 3}
    )
```
where `Coord(i=0, j=1)` is point 1, `Coord(i=5, j=3)` is point 2, `Coord(i=13, j=5)` is point 3, and `Coord(i=14, j=7)` is point 4. Nested within the dictionary we also store the number of steps it takes to reach this point of the path from the previous node.

### Creating the adjacency list

Creating the adjacency list with edge contraction first requires finding decision points. I created this data by iterating through all grid tiles, and if a grid tile had more than two neighbours it was declared a decision point and was therefore added to a list of coordinates for further processing.

Once the list of decision points is found, the construction of the adjacency list could begin. For each decision point, we get a dictionary that tells us for each neighbour how far away the point is. We only connect neighbours that are directly adjacent as this would violate our no backtracking constraint. To enforce no backtracking, for each decision point we breadth-first search outwards and stop propagating when we reach the next neighbours.

The graph encoded through the adjacency list is directed because as we look for neighbouring points, we stop traversing a route if we try to move up a slope. 

To create the adjacency list we use depth-first search using a stack. We could alternatively use BFS with a queue. Traversing through the tiles in our graph starting from each decision point, we add the point to our adjacency list if the tile we have traversed to is a decision point and not the starting point. If this is not the case, we add the tile to the set of visited tiles, and append the next possible immediate tiles from this coordinate that we can validly step to. Once the stack is empty, we start the iteration again at the next decision point.

Once the decision points have been iterated over, we have successfully constructed our complete adjacency list, and we can depth-first search to find the longest path.

### Depth-First Search

To find the longest path, we use depth-first search from the starting tile. Negative infinity is used as the starting distance because this means that if an edge can not find an exit through any route it will have a distance of negative infinity. This propagates as any paths that do not lead to an exit get their distance dominated by the negative infinity term. Therefore, **any** valid path will beat a shorter path that can never find an exit. This would not be the case if we set it to zero.

## Part 2

In part 2, we are now told to treat the slopes as regular path tiles. This increases the size of the problem tremendously.

Thankfully, because we utilized edge contraction in the solution to part 1, this change is very easy. It only requires reinterpreting the input slope tiles as regular path tiles and re-running the same algorithm as used in part 1. Though not optimal, this finds the most scenic path in a reasonable amount of time (~1 minute).

## Improvements

<!-- ### Part 1 -->

### Part 2

I think topological sort could be used to solve part 2 in linear time. I will have to read more about topological sort before attempting this.

### Algorithms

A nice application of depth-first search to solving a graph pathfinding problem.

### Software Engineering

I think overall my code is a nicely written solution to this problem.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday23.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>