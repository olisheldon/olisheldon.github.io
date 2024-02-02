---
title: "Day 20: Pulse Propagation"
description: Graph with state <br/> Difficulty ★★★
layout: nested
---

# Day 20: Pulse Propagation

[**link**](https://adventofcode.com/2023/day/20)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day20.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day20.py)

## Description

This problem requires modelling a system of communication modules connected to each other. These modules communicate through pulses that can be HIGH or LOW. Each module has a number of destination modules that it sends its ouput pulse to.

This system of modules forms a graph.

### Module Types

The following are the types of modules within the problem:

#### Flip-Flop

 - Symbol: %
 - State: On / Off
 - Default state: Off

`Flip-flop modules (prefix %) are either on or off; they are initially off. If a flip-flop module receives a high pulse, it is ignored and nothing happens. However, if a flip-flop module receives a low pulse, it flips between on and off. If it was off, it turns on and sends a high pulse. If it was on, it turns off and sends a low pulse.`
(From AoC day 20 description)

#### Conjunction

 - Symbol: &
 - State: On / Off
 - Default state: Off

`Conjunction modules (prefix &) remember the type of the most recent pulse received from each of their connected input modules; they initially default to remembering a low pulse for each input. When a pulse is received, the conjunction module first updates its memory for that input. Then, if it remembers high pulses for all inputs, it sends a low pulse; otherwise, it sends a high pulse.`
(From AoC day 20 description)

#### Starter modules

There is a single broadcast module (named broadcaster). When it receives a pulse, it sends the same pulse to all of its destination modules. There is also a module with a single button on it called the button module. When you push the button, a single low pulse is sent directly to the broadcaster module.

### Processing Order

It is the case that pulses are always processed in the order that they are sent. So, if for example a pulse is sent to modules `a` and `b`, then module `a` processes its pulse and sends more pulses. But, before these new pulses are processed the pulse sent to `b` must be processed first.

This means the pulses are pushed to a queue, and pulses are processed from the front of the queue. This is a first-in-first-out (FIFO) data structure.

### Example

There are a number of very nice examples on the [**Advent of Code website**](https://adventofcode.com/2023/day/20) that I implore you to read before continuing to my solutions.

The most important idea to note from these examples is the idea that pushing the button does not always produce the same same series of pulses sent between each module. As the nodes within the graph contain state that affect the way the module reacts to an incoming pulse, the messages created from pressing the button does not only depend on the structure of the graph but also the state of each node within the graph.

## Part 1

For part 1, we must build the graph from a list of strings of form:

```
~name -> list[name]
```

where `~` is the module type, `name` is the modules name (used for linking between modules), and `list[name]` are the names of the destination modules. 

Once the graph is built, we push the button module 1000 times. Throughout these button presses, a number of low and high pulses are sent. We must count these pulse types individually and return their product.

To model this I created a 'Motherboard' class that contained all modules within. The modules could then communicate through this Motherboard class. To send messages to each other, a 'Message' class was created that held state of:

 - PulseType (HIGH or LOW)
 - source_name (where the message is coming from)
 - destination_name (where the message is going)

 On creation of this message class, static tallies for the number of high and low pulses that were created was tallied. 




## Part 2

Part 2 has us consider the same system of modules, but instead we must find the fewest number of button presses before a message is sent containing a low pulse to the module 'rx'.

At this point within the Advent of Code, the solution to this problem is not going to be just iterate the first solution until you find the message with the correct pulse type and destination (In frustration I tried this for ~1 hour and didn't find the solution).

I have not yet completed this part of Day 20's challenge, but I do have a few ideas that I will pursue to solve it:

 - The easiest solution would be manual analysis. This analysis would require looking at the modules that contain rx as a destination and analysing these. In the end, the solution is very likely to take the form of finding looping states that create the message I am looking for.
 - Consider grouping together multiple nodes to reduce the size of the graph. This will make the analysis easier. This will involves analysing subgraphs such as FlipFlop->FlipFlop, Conjunction->Conjunction, FlipFlop->Conjunction and so on. I think through this the problem can be made more simple, and perhaps caching could be employed for subgraphs. 
 - Find an approach that automatically finds cycles within the graph, and uses these to compute the answer after a number of iterations.

## Improvements

### Part 1

I think my solution is quite bloated with the number of classes to model this system. However, this does make debugging very nice; For example, my `Message` class can perfectly replicate the Message logging presented on the [**Advent of Code website**](https://adventofcode.com/2023/day/20).

```
button -low-> broadcaster
broadcaster -low-> a
broadcaster -low-> b
broadcaster -low-> c
a -high-> b
b -high-> c
c -high-> inv
inv -low-> a
a -low-> b
b -low-> c
c -low-> inv
inv -high-> a
```

### Part 2

### Algorithms

### Software Engineering

Each module has a basic function of accepting a message and returning new messages. To create this generic interface of handling messages, I created ana abstract base class for the modules (ModuleBase), which defined an interface for all modules within the motherboard to use. This use of an abstract base class also prevented code duplication, an example of this is the `__repr__` for each module.

## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday20.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>