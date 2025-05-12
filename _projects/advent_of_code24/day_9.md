---
title: "Day 9: Disk Fragmenter"
description: File Compaction <br/> Difficulty ★★
layout: nested
---

# Day 9: Disk Fragmenter

[**link**](https://adventofcode.com/2024/day/9)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day9.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day9.py)

## Description

This problem involves manipulating a disk map representation. The input is a sequence of numbers where alternating digits represent file lengths and free space lengths. We need to compact the disk by moving file blocks and then calculate a checksum based on their positions.

For example, a disk map like `12345` would represent a one-block file, two blocks of free space, a three-block file, four blocks of free space, and then a five-block file. Using one character for each block where digits are the file ID and `.` is free space, this would look like:

```
0..111....22222
```

## Part 1

In Part 1, we move blocks one at a time from the end of the disk to the leftmost free space. The solution first expands the disk map into individual blocks, then uses a two-pointer approach to move blocks from right to left:

```python
def part1():
    expanded = []
    for i, count in enumerate(disk_map):
        if i % 2:
            expanded += [EMPTY] * count
        else:
            expanded += [i // 2] * count

    l, r = 0, len(expanded) - 1
    while l < r:
        if expanded[l] != EMPTY:
            l += 1
        elif expanded[r] == EMPTY:
            r -= 1
        else:
            expanded[l] = expanded[r]
            expanded[r] = EMPTY
            l += 1
            r -= 1
    expanded = list(filter(lambda x: x != EMPTY, expanded))
    return checksum(expanded)
```

This approach:
1. Creates an expanded representation of the disk where each position is either a file ID or marked as empty (-1)
2. Uses two pointers (l and r) to find empty spaces from the left and file blocks from the right
3. Moves blocks one by one by swapping elements
4. Removes all empty blocks and calculates the final checksum

The checksum is calculated by summing the product of each block's position with its file ID:

```python
def checksum(nums):
    return sum(i * num for i, num in enumerate(nums))
```

## Part 2

For Part 2, we now move entire files instead of individual blocks. We attempt to move each file once, in order of decreasing file ID, to the leftmost span of free space that can fit the entire file:

```python
def part2():
    files = {}
    blanks = []
    
    file_id = 0
    position = 0
    
    for i, count in enumerate(disk_map):
        if i % 2 == 0:
            files[file_id] = (position, count)
            file_id += 1
        else:
            blanks.append((position, count))
        position += count
    
    for fid in range(file_id - 1, -1, -1):
        pos, size = files[fid]
        
        best_pos = -1
        best_blank_idx = -1
        
        for i, (blank_pos, blank_len) in enumerate(blanks):
            if blank_pos >= pos:
                break
                
            if blank_len >= size:
                best_pos = blank_pos
                best_blank_idx = i
                break
        
        if best_pos != -1:
            files[fid] = (best_pos, size)
            
            if size == blanks[best_blank_idx][1]:
                blanks.pop(best_blank_idx)
            else:
                blanks[best_blank_idx] = (best_pos + size, blanks[best_blank_idx][1] - size)
    
    total = 0
    for fid, (pos, size) in files.items():
        for x in range(pos, pos + size):
            total += fid * x
            
    return total
```

This approach:
1. Builds a dictionary of files (`{file_id: (position, size)}`) and a list of free space segments
2. Processes files in descending ID order (starting with the highest ID)
3. For each file, finds the leftmost suitable free space that can fit the entire file
4. Updates file positions and free space segments accordingly
5. Calculates the checksum based on final file positions

## Improvements

The solution handles both parts efficiently, with a time complexity of O(n) for both parts, where n is the total size of the disk. Some potential improvements:

- More descriptive variable names could make the code more readable
- Additional comments would help explain the logic
- An alternative approach for Part 2 could track filled positions rather than calculating the checksum by iterating through every position
- The checksum calculation in Part 2 could be optimized to avoid iterating through every block position

### Algorithms

The solution uses:
- Two-pointer technique in Part 1 to efficiently move blocks from right to left
- Greedy algorithm in Part 2 to move files to the leftmost viable free space
- Dictionary-based tracking of file and free space positions

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday9.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
