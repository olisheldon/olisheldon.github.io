---
title: "Day 18: Lavaduct Lagoon"
description: Polygon properties, Mixin <br/> Difficulty ★★
layout: nested
---

# Day 18: Lavaduct Lagoon

[**link**](https://adventofcode.com/2023/day/18)

[**input**](https://github.com/olisheldon/AdventOfCode23/blob/main/data/day18.txt)

[**my solution**](https://github.com/olisheldon/AdventOfCode23/blob/main/day18.py)

## Description

For this problem, we must interpret a *dig plan*. The dig plan takes the form a list of instructions, with each instruction containing:

 - Direction (U, R, D, L)
 - Length (integer)
 - Colour (hexademical)

 A digger follows this dig plan, starting in a 1m^3 hole and proceeding to dig following the dig plan. Each instruction tells the digger to dig in a direction for a certain length. The dig plan is guaranteed to draw a closed shape.

## Part 1

We follow the dig plan to draw the edge of a 2D polygon. After this is done, we proceed to dig out the interior. Finally, we must return the total area digged.

My solution to this uses *shoelace formula* and *Pick's theorem*.

### [Shoelace Formula](https://en.wikipedia.org/wiki/Shoelace_formula)

Shoelace formula allows you to compute the area of a polygon given its integer coordinates:

![Shoelace Formula](https://wikimedia.org/api/rest_v1/media/math/render/svg/b7d97cd80984bcfc229f3a100ba098db6311950c "Shoelace Formula")

### [Pick's Theorem](https://en.wikipedia.org/wiki/Pick%27s_theorem)

Pick's Theorem allows you to find the area of a polygon with integer vertex coordinates as a function of the integer points within it and on its boundary.

![Pick's Theorem](https://wikimedia.org/api/rest_v1/media/math/render/svg/697592698c914435d23b1bae29e02dd14dfea9c7 "Pick's Theorem")


Using these two theorem I solved the problem. This approach to the problem is nice as it is very simple to convert between the input (direction, number of step pairs) to a list of integer vertex coordinates that define a polygon that Shoelace formula and Pick's theorem can use.

## Part 2

Part 2 only changes the polygon shape. This is done by reinterpreting the input to give new instructions to the digger. The new instructions, containg direction and step pairs, are parsed through the colour.

The instructions are parsed from the hexademical colour values as follows:

 - The first five hexadecimal digits encode the distance in meters as a five-digit hexadecimal number
 - The last hexadecimal digit encodes the direction to dig: 0 means R, 1 means D, 2 means L, and 3 means U.

This change increases the size of the polygon by a large amount. Thankfully, the time complexity of my solution to part 1 is `O(N)`, where N is the number of instructions. Therefore, the same solution can be reused for part 2 with the same (optimal) time complexity.

## Improvements

I think my solutions to part 1 and 2 are optimal. 

### Algorithms

Shoelace formula and Pick's theorem are formulae that I have never come across before, but were found through searching for formulae concerning the area of polygons. They are very nice ways to approach problems that consider areas of Polygons.

### Software Engineering

I like the way that I wrote my solution to this problem. As part 1 and part 2 differ only in their conversion from `input -> list[Instruction(Direction, Steps)]`, my Digger class contains a method `dig` that accepts these instructions on construction and returns the area dug out when called. 

As such, I created a dataclass that is accepted by the Digger class

```python
@dataclass
class Instruction:
    direction: Direction
    steps: int
```

Then, using the Mixin 

```python
@dataclass
class ColourMixin:
    colour: str
```

I created two dataclasses, `DigPlan` for part 1 interpretation of the input and `ColourInstruction` for part 2.

```python
@dataclass
class DigPlan(ColourMixin, Instruction):
    pass


@dataclass
class ColourInstruction(ColourMixin, Instruction):

    def __post_init__(self):
        self.steps = int(self.colour[:-1], base=16)
        ending_colour = self.colour[-1]
        match ending_colour:
            case '0':
                direction = Direction.R
            case '1':
                direction = Direction.D
            case '2':
                direction = Direction.L
            case '3':
                direction = Direction.U
            case _:
                raise RuntimeError(
                    f"{self.__class__.__name__} ending digit {ending_colour} is not recognised.")
        self.direction = direction
```

This resulted in very clean code for users of the Digger class.


## Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2FAdventOfCode23%2Fblob%2Fmain%2Fday18.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>