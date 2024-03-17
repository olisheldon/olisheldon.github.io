---
title: "Day 20: Pulse Propagation"
description: Graph with state <br/> Difficulty ★★★
layout: nested
---

# Day 20: Pulse Propagation

[**link**](https://adventofcode.com/2023/day/20)

[**input**](https://adventofcode.com/2023/day/20/input)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/python/day20.py)

## Description

This problem requires modelling a system of communication modules connected to each other. These modules communicate through pulses that can be HIGH or LOW. Each module has a number of destination modules that it sends its ouput pulse to.

This system of modules forms a graph.

### Module Types

The following are the types of modules within the problem:

#### Flip-Flop

 - Symbol: %
 - State: On / Off
 - Default state: Off

'Flip-flop modules (prefix %) are either on or off; they are initially off. If a flip-flop module receives a high pulse, it is ignored and nothing happens. However, if a flip-flop module receives a low pulse, it flips between on and off. If it was off, it turns on and sends a high pulse. If it was on, it turns off and sends a low pulse.'
(From AoC day 20 description)

#### Conjunction

 - Symbol: &
 - State: On / Off
 - Default state: Off

Conjunction modules (prefix &) remember the type of the most recent pulse received from each of their connected input modules; they initially default to remembering a low pulse for each input. When a pulse is received, the conjunction module first updates its memory for that input. Then, if it remembers high pulses for all inputs, it sends a low pulse; otherwise, it sends a high pulse. 
(From AoC day 20 description)

#### Starter modules

There is a single broadcast module (named broadcaster). When it receives a pulse, it sends the same pulse to all of its destination modules. There is also a module with a single button on it called the button module. When you push the button, a single low pulse is sent directly to the broadcaster module.

### Processing Order

It it the case that pulses are always processed in the order they are sent. So, if for example a pulse is sent to modules `a` and `b`, then module `a` processes its pulse and sends more pulses. But, before these new pulses are processed the pulse sent to `b` must be processed first.

This means the pulses are pushed to a queue, and pulses are processed from the front of the queue. This is a first-in-first-out (FIFO) data structure.

### Example

There are a number of very nice examples on the Advent of Code website that I implore you to read before continuing.

The most important idea to note from these examples is the idea that pushing the button does not always produce the same same series of pulses sent between each module. As the nodes within the graph contain state that affect the way the module reacts to an incoming pulse, the messages created from pressing the button does not just depend on the structure of the graph but also the state of each node within the graph.

## Part 1

For part 1, we must build the graph from a list of strings of form:

```
~name -> list[name]
```

where `~` is the module type, `name` is the modules name (used for linking between modules), and `list[name]` are the names of the destination modules. 

For part 1, we must build the graph as given and push the button module 1000 times. Throughout these button presses, a number of low and high pulses are sent. We must count these pulse types individually and return their product.



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
 - Consider grouping together multiple nodes to reduce the size of the graph. This will make the analysis easier. This will involves analysing subgraphs such as FlipFlop->FlipFlop, Conjunction->Conjunction, FlipFlop->Conjunction and so on. I think through this the problem can be made more simple.
 - 

## Improvements

### Part 1

### Part 2

### Algorithms

### Software Engineering

#### Part 1

Each module has a basic function of accepting a message and returning new messages. To create this generic interface of handling messages, I created ana abstract base class for modules (ModuleBase), which defined an interface for all modules within the motherboard to use. 