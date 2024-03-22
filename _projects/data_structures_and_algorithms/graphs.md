---
title: Graphs
description: Representations, DFS Traversal, BFS Traversal, Visualization, Backtracking, Shortest Path
layout: nested
---

# Graphs

A graph constists of a set of vertices and a set of edges that connects vertices. These edges can be either directed or undirected, leading to directed and undirected graphs. 

## Representations

Common data structures to represent graphs are:

 - Matrix
 - Adjacency Matrix
 - Adjacency List

### Matrix

Graphs are commonly represented visually in matrices. Below is a 4 x 4 matrix representing a graph. If we interpret zeros as free space and ones as blocked and assume we can move freely between the free spaces, this matrix represents a graph of 12 vertices with 12 edges. 

```
[ [ 0, 0, 0, 0],
  [ 1, 1, 0, 0],
  [ 0, 0, 0, 1],
  [ 0, 1, 0, 0] ]
```

### Adjacency Matrix

The adjacency matrix is a square matrix that directly shows the connectivity between vertices. It does this by having each element `A_ij" showing the connectivity between vertex i and vertex j; this value is zero when there is no edge.

If the graph is undirected, this matrix is symmetric.

### Adjacency List

Commonly represented by either

```python
class GraphNode:

    def __init__(self, val: int):
        self.val: int = val
        self.neighbours: list[GraphNode] = []
```

or

```python
graph: dict[str, list[str]] = {"A" : [ ... ], "B" : [ ... ], ...}
```

## Converting between representations



# Traversal

Graphs are commonly traversed using depth-first search and breadth-first search. Very similar techniques to backtracking.

## Matrix DFS

Q: What are the number of unique paths from the top left to the bottom right of a matrix, with the constraint that the same matrix element can not be visited twice?

```python
grid = [[0, 0, 0, 0],
        [1, 1, 0, 0],
        [0, 0, 0, 1],
        [0, 1, 0, 0]]

# Count paths (backtracking)
def dfs(grid: list[list[int]], coords: tuple[int, int], visit: set[int]) -> int:

    row, col = coords
    ROWS, COLS = len(grid), len(grid[0])
    if (min(row, col) < 0 or
        row == ROWS or col == COLS or
        (row, col) in visit or grid[row][col] == 1):
        return 0
    if row == ROWS - 1 and col == COLS - 1:
        return 1

    visit.add((row, col))

    count = 0
    count += dfs(grid, row + 1, col, visit)
    count += dfs(grid, row - 1, col, visit)
    count += dfs(grid, row, col + 1, visit)
    count += dfs(grid, row, col - 1, visit)

    visit.remove((row, col))

    return count

print(dfs(grid, (0, 0), set()))
```

Time complexity O(4**(rows + columns)) = O(4**N)

### DFS Tree Visualization

TODO

## Matrix BFS

Q: What is the length of the shortest path from the top left of the grid to the bottom?

We could reuse our DFS algorithm but this is a brute-force approach and very inefficient. With BFS we can solve this problem in linear time (O(N)). BFS requires the use of a queue data structure, allowing efficient popping from one end and efficient pushing to the other. This gives us a data structure with a first-in-first-out (FIFO) property.

<!-- ## Visualization -->

## Code

```python
from collections import deque

# Matrix (2D Grid)
grid = [[0, 0, 0, 0],
        [1, 1, 0, 0],
        [0, 0, 0, 1],
        [0, 1, 0, 0]]

def bfs(grid: list[list[int]]) -> :
    ROWS, COLS = len(grid), len(grid[0])
    visit = set()
    queue = deque()
    queue.append((0, 0))
    visit.add((0, 0))

    length = 0
    while queue:
        for i in range(len(queue)):
            r, c = queue.popleft()
            if r == ROWS - 1 and c == COLS - 1:
                return length

            neighbours = [[0, 1], [0, -1], [1, 0], [-1, 0]]
            for dr, dc in neighbours:
                if (min(r + dr, c + dc) < 0 or
                    r + dr == ROWS or c + dc == COLS or
                    (r + dr, c + dc) in visit or grid[r + dr][c + dc] == 1):
                    continue
                queue.append((r + dr, c + dc))
                visit.add((r + dr, c + dc))
        length += 1
    return length

print(bfs(grid))
```


## Adjacency List


### Building an adjacency list

How to build adjacency list from directed edges:

```python
# Python makes this very easy with default dict
from collections import defaultdict


edges: list[tuple[str, str]] = [("A", "B"), ("B", "C"), ("B", "E"), ("C", "E"), ("E", "D")]

adj_list: dict[str, str] = defaultdict(list)

for src, dst in edges:
    adj_list[src].append(dst)
```

## DFS Backtracking

```python
# Counting paths
def dfs(node: str, target: str, adj_list: dict[str, list[str]], visit: set[str]) -> int:
    if node in visit:
        return 0
    if node == target:
        return 1
    
    count = 0
    visit.add(node)
    for neighbour in adj_list[node]:
        count += dfs(neighbour, target, adj_list, visit)
    visit.remove(node)

    return count
```

TODO: Draw decision tree

Time complexity: O(N**V) where N is the average number of edges per vertex and V is the number of vertices.

## BFS Shortest Path

```python
from collections import deque

# Shortest path length from node to target
def bfs(node: str, target: str, adj_list: dict[str, list[str]]):
    length = 0
    visit = set()
    visit.add(node)
    queue = deque()
    queue.append(node)

    while queue:
        for i in range(len(queue)):
            curr = queue.popleft()
            if curr == target:
                return length

            for neighbour in adj_list[curr]:
                if neighbour not in visit:
                    visit.add(neighbour)
                    queue.append(neighbour)
        length += 1

print(bfs("A", "E", adj_list))
```

TODO: Show example

Time complexity: O(V + E)
Memory complexity: O(V) (All nodes in set and all nodes in queue)