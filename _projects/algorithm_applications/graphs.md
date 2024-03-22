---
title: Graphs
description: Dijkstra's, Kruskal's (MST), Topological Sort
layout: nested
---

# Graphs

## Dijkstra's Algorithm

Question: What is the shortest path from one node to another?

Idea: Frontier of nodes that we have calculated shortest-path for so far.

Time complexity:
 - For V nodes, there are max `V**2` edges as each node can be at most connected to all other nodes.
 - When pushing and poping from minheap, the size of worst case heap is number of edges (`V**"`). Therefore, `log(E)`. 
 - We may have to do this operation for all edges, therefore `O(ElogE) = O(Elog(V**2)) = O(ElogV)`.

The code is very similar to BFS.

```python
import heapq

# Given a connected graph represented by a list of edges, where
# edge[0] = src, edge[1] = dst, and edge[2] = weight,
# find the shortest path from src to every other node in the 
# graph. There are n nodes in the graph.
# O(E * logV), O(E * logE) is also correct.
def shortest_path(edges, n, src):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
        
    # s = src, d = dst, w = weight
    for s, d, w in edges:
        adj[s].append([d, w])

    shortest = {}
    min_heap = [[0, src]]
    while min_heap:
        w1, n1 = heapq.heappop(min_heap)
        if n1 in shortest:
            continue
        shortest[n1] = w1

        for n2, w2 in adj[n1]:
            if n2 not in shortest:
                heapq.heappush(min_heap, [w1 + w2, n2])
    return shortest
```


### Prim's Algorithm (Minimum Spanning Tree)

This is very similar to Dijkstras. 

For undirected graphs it is basically just a tree.
Graph is cyclical
For connected graphs (all nodes are reachable).

A minimum spanning tree is a subset of the edges that form a tree based on this critieria s.t. we minimize the total cost.
For N nodes to be connected such that there are no cycles requires N-1 edges. 
The algorithm can start at any node. 

Data structures required:
 - Visit (hashset)
 - MinHeap (wgt, n1, n2)

<!-- VISUALIZATION -->

Just as it is very similar to Dijkstras in structure, so it is in time complexity:
 - Time complexity: `O(ElogV)`
 - Memory complexity: `O(E)` (from MinHeap)

```python
import heapq

# Given a list of edges of a connected undirected graph,
# with nodes numbered from 1 to n,
# return a list edges making up the minimum spanning tree.
def minimum_spanning_tree(edges, n):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
    for n1, n2, weight in edges:
        adj[n1].append([n2, weight])
        adj[n2].append([n1, weight])

    # Initialize the heap by choosing a single node
    # (in this case 1) and pushing all its neighbours.
    min_heap = []
    for neighbour, weight in adj[1]:
        heapq.heappush(min_heap, [weight, 1, neighbour])

    mst = []
    visit = set()
    visit.add(1)
    while len(visit) < n:
        weight, n1, n2 = heapq.heappop(min_heap)
        if n2 in visit:
            continue

        mst.append([n1, n2])
        visit.add(n2)
        for neighbour, weight in adj[n2]:
            if neighbour not in visit:
                heapq.heappush(min_heap, [weight, n2, neighbour])
    return mst
```

## Kruskal's Algorithm (Minimum Spanning Tree)

Greedy algorithm like Dijkstra and Prims.

Uses Union-Find data structure

Idea: Take all edges, and add minimum weight edges to minimum spanning tree. Union the edges together to 'connect' them.

```python
import heapq 

class UnionFind:
    def __init__(self, n):
        self.par = {}
        self.rank = {}

        for i in range(1, n + 1):
            self.par[i] = i
            self.rank[i] = 0
    
    # Find parent of n, with path compression.
    def find(self, n):
        p = self.par[n]
        while p != self.par[p]:
            self.par[p] = self.par[self.par[p]]
            p = self.par[p]
        return p

    # Union by height / rank.
    # Return false if already connected, true otherwise.
    def union(self, n1, n2):
        p1, p2 = self.find(n1), self.find(n2)
        if p1 == p2:
            return False
        
        if self.rank[p1] > self.rank[p2]:
            self.par[p2] = p1
        elif self.rank[p1] < self.rank[p2]:
            self.par[p1] = p2
        else:
            self.par[p1] = p2
            self.rank[p2] += 1
        return True

# Given an list of edges of a connected undirected graph,
# with nodes numbered from 1 to n,
# return a list edges making up the minimum spanning tree.
def minimumSpanningTree(edges, n):
    minHeap = []
    for n1, n2, weight in edges:
        heapq.heappush(minHeap, [weight, n1, n2])

    unionFind = UnionFind(n)
    mst = []
    while len(mst) < n - 1:
        weight, n1, n2 = heapq.heappop(minHeap)
        if not unionFind.union(n1, n2):
            continue
        mst.append([n1, n2])
    return mst
```

## Topological Sort

<!-- Visualization -->

Topological sort: For every edge (strictly directed). Guarantees source node comes before the destination node in the topological sort result. 

Graphs must be directed *and* acyclical (DAG).

Can choose to implement with DFS or BFS. 

<!-- Explanation with visualization! -->

```python
# Given a directed acyclical graph, return a valid
# topological ordering of the graph. 
def topological_sort(edges, n):
    adj = {}
    for i in range(1, n + 1):
        adj[i] = []
    for src, dst in edges:
        adj[src].append(dst)

    top_sort = []
    visit = set()
    for i in range(1, n + 1):
        dfs(i, adj, visit, top_sort)
    top_sort.reverse()
    return top_sort

def dfs(src, adj, visit, top_sort):
    if src in visit:
        return
    visit.add(src)
    
    for neighbour in adj[src]:
        dfs(neighbour, adj, visit, top_sort)
    top_sort.append(src)
```

If we would like this algorithm to work with cyclical graphs (detect and reject), we would need to have another hashset 'path'.

An application for an algorithm like this could be University courses pre-requisite checking.