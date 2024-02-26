---
title: Graphs
description: INCOMPLETE - complete adjacency list/matrix and conversion
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

