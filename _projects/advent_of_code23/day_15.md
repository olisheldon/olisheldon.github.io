---
title: "Day 15: Lens Library"
description: Hashing <br/> Difficulty ★
layout: nested
---

# Day 15: Lens Library

[**link**](https://adventofcode.com/2023/day/15)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day15.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day15.py)

## Description

In this problem we consider an _initialization sequence_, a comma separated list of instructions to process. 

An example of this *initialization sequence* (`lkb-,dncgk=5, ...`) shows two instructions. Instructions can take two possible forms:

 - `<name>=<number>`
 - `<name>-`



## Part 1

In part 1, we are asked to us write a simple hashing function to map the string associated with each instruction to an integer in `[0, 256)`.

We return the sum of the hash value of each instruction, to show that the hashing functions properly.

## Part 2

Part 2 adds 256 boxes numbered in `[0, 256)`.

The hash of the string contained within each instruction is the index of the box the instruction belongs in. 

Instructions may contain either a '-' or '=' sign, indicating the operation to apply to the boxes.

 - '-' : Move to the relevant box, and remove the lens with the given label if it is present in the box, then move any remaining lenses forward in the box. This instruction has no affect if the given label is not present within the box. 
 - '=' : Instructions containing an equals sign are followed by an integer that should be interpreted as a 'focal length'. If a lens with the same label is already present, replace the old lens with the new lens. Otherwise, if there is not a lens with that label in the box, add the lens to the back of the box. 

After interpreting the entire sequence, return the total _focusing power_ of all of the lenses. The focusing power of a single lens is the product of:

 - One plus the box number of the lens in question.
 - The slot number of the lens within the box: 1 for the first lens, 2 for the second lens, and so on.
 - The focal length of the lens.

The solution is the sum of the focusing powers for each lens in the boxes.

In my solution, I implemented the boxes as a list of list of strings, of total length 256. The focal length of the appropriate instructions is stored in a dictionary mapping the string/name within the instruction to the correct value.

## Improvements

<!-- ### Part 1 -->

### Part 2

This problem was quite simple, but was difficult to write in a simple way. I decided to make use of Python's abstract base class library _abc_ to create separate '-' and '=' classes that shared the same interface.

This allowed for the class instance representing the boxes and focal lengths to be passed to the instructions, creating inversion of control as the Boxes class has no knowledge of the individual SequenceElement classes.

My only issue with part 2 of this problem was my choice to implement the boxes as a list of lists. As the problem requires us to remove elements from anywhere within these structures, we will be removing elements from the list structure. As the lists are not sorted, this takes O(N) time. This leads to a time complexity of O(N**2). Could this be improved?

<!-- ### Algorithms -->

### Software Engineering

It was nice to use an abstract base class to define an interface for the instructions. This resulted in nice, readable code.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday15.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>