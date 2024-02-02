---
title: Trie
description: Prefix Tree, Union-Find, Segment Tree, Iterative DFS
layout: nested
---

# Trie (Prefix Tree)

A Trie is a tree of characters.

Every node has a value and a hashmap of its children, where the key is the character.

Performance:

Insert word: O(1)
Search word: O(1)
Search prefix: O(1) -> Makes it unique from hashmaps.

```python
class TrieNode:
    def __init__(self):
        self.children: dict[str, TrieNode] = {}
        self.word: bool = False
    
class Trie:
    def __init__(self):
        self.root: TrieNode = TrieNode()
    
    def insert(self, word: str) -> None:
        curr = self.root
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        curr.word = True
    
    def search(self, word: str) -> bool:
        curr = self.root
        for c in word:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return curr.word

    def starts_with(self, prefix: str) -> None
        curr = self.root
        for c in word:
            if c not in curr.children:
                return False
            curr = curr.children[c]
        return True
```


## Applications

### Union-Find (Disjoint Sets)

Determine if a graph has a cycle. This can also be achieved with depth-first search (but how does efficiency compare?).

We want to 'union by height'. i.e. We take the smaller tree and add it as a child of the larger tree as this is more balanced.

Union find does not claim to accurately represent a graph, only detect ccyles and count number of connected componenets.

```python
class UnionFind:
    def __init__(self, n: int):
        self.par: dict[int, int] = {}
        self.rank: dict[int, int] = {}

        for i in range(1, n + 1):
            self.par[i] = i
            self.rank[i] = 0
    
    def find(self, n: int) -> int:
        p = self.par[n]
        while p != self.par[p]:
            self.par[p] = self.par[self.par[p]]
            p = self.par[p]
        return p

    def union(self, n1: int, n2: int) -> bool:
        '''
        Return false if already connected, true otherwise.
        '''
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
```

### Segment Tree

Segment trees taken an array and segments it. The resulting structure looks similar to a heap, except the structure property does not hold. Like a heap, it can also be implemented using an array, however with the absence of the structure property it has a much more complicated implementation.

```python
class SegmentTree:
    def __init__(self, total: int, l: int, r: int):
        self.sum: int = total
        self.left: SegmentTree | None = None
        self.right: SegmentTree | None = None
        self.l: int = l
        self.r: int = r
        
    # O(n)
    @staticmethod
    def build(nums: list[int], l: int, r: int) -> 'SegmentTree':
        if l == r:
            return SegmentTree(nums[l], l, r)

        M = (l + r) // 2
        root = SegmentTree(0, l, r)
        root.left = SegmentTree.build(nums, l, M)
        root.right = SegmentTree.build(nums, M + 1, r)
        root.sum = root.left.sum + root.right.sum
        return root

    # O(logn)
    def update(self, index: int, val: int) -> None:
        if self.l == self.r:
            self.sum = val
            return
        
        M = (self.l + self.r) // 2
        if index > M:
            self.right.update(index, val)
        else:
            self.left.update(index, val)
        self.sum = self.left.sum + self.right.sum
        
    # O(logn)
    def range_query(self, l: int, r: int) -> int:
        if l == self.l and r == self.r:
            return self.sum
        
        M = (self.l + self.r) // 2
        if l > M:
            return self.right.range_query(l, r)
        elif r <= M:
            return self.left.range_query(l, r)
        else:
            return (self.left.range_query(l, M) +
                    self.right.range_query(M + 1, r))
```

### Iterative DFS

Three kinds: 
 - in_order
 - pre_order
 - post_order

 ```python
 class TreeNode:
    def __init__(self, val: int, left: int, right: int):
        self.val = val
        self.left = left
        self.right = right
 ```

All algorithms that use recursion (including DFS) use the call stack to move to the correct nodes. To do it iteratively, we must declare our own stack. 

#### In Order

```python
# Time and space: O(n)
def inorder(root: TreeNode) -> None:
    stack = []
    curr = root

    while curr or stack:
        if curr:
            stack.append(curr)
            curr = curr.left
        else:
            curr = stack.pop()
            print(curr.val)
            curr = curr.right
```

#### Pre Order

```python
# Time and space: O(n)
def pre_order(root: TreeNode) -> None:
    stack = []
    curr = root
    while curr or stack:
        if curr:
            print(curr.val)
            if curr.right:
                stack.append(curr.right)
            curr = curr.left
        else:
            curr = stack.pop()
```

#### Post Order

```python
# Time and space: O(n)
def post_order(root: TreeNode) -> None:
    stack = [root]
    visit = [False]
    while stack:
        curr, visited = stack.pop(), visit.pop()
        if curr:
            if visited:
                print(curr.val)
            else:
                stack.append(curr)
                visit.append(True)
                stack.append(curr.right)
                visit.append(False)
                stack.append(curr.left)
                visit.append(False)
```