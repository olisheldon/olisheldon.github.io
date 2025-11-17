---
title: "Day 17: Chronospatial Computer"
description: 3-bit computer simulation and reverse engineering <br/> Difficulty ★★★
layout: nested
---

# Day 17: Chronospatial Computer

[**link**](https://adventofcode.com/2024/day/17)

[**input**](https://github.com/olisheldon/aoc24/blob/main/data/day17.txt)

[**my solution**](https://github.com/olisheldon/aoc24/blob/main/python/day17.py)

## Description

This problem presents us with a 3-bit computer simulator that operates on programs consisting of 3-bit numbers (0-7). The computer has three registers (A, B, C) that can hold any integer, an instruction pointer, and supports eight different opcodes. The challenge involves both simulating the computer's execution and reverse-engineering a specific input that produces a quine (a program that outputs itself).

The computer executes instructions sequentially, with each instruction consisting of an opcode and an operand. The instruction pointer advances by 2 after each instruction (except for jump instructions), and the program halts when trying to read past the end of the program.

## Part 1

Part 1 requires implementing a complete computer simulator that can execute the eight different opcodes:

- **ADV (0)**: Division - divides register A by 2^(combo operand) and stores in A
- **BXL (1)**: Bitwise XOR - XORs register B with literal operand
- **BST (2)**: Modulo store - stores (combo operand % 8) in register B
- **JNZ (3)**: Jump if not zero - jumps to literal operand if A ≠ 0
- **BXC (4)**: XOR B and C - XORs registers B and C, stores in B
- **OUT (5)**: Output - outputs (combo operand % 8)
- **BDV (6)**: Division to B - like ADV but stores result in B
- **CDV (7)**: Division to C - like ADV but stores result in C

The key implementation detail is understanding combo operands: values 0-3 are literal, while 4-6 refer to registers A, B, C respectively (value 7 is invalid).

## Part 2

Part 2 presents a significantly more complex challenge: finding the lowest positive value for register A that causes the program to output a copy of itself. This is essentially solving for a quine condition.

The solution employs a sophisticated reverse-engineering approach:

1. **Validation First**: The algorithm validates that the program follows expected patterns (ends with JNZ 0, has exactly one ADV instruction with operand 3)

2. **Bit-by-bit Construction**: Rather than brute-forcing all possible values, the solution builds the answer 3 bits at a time, working backwards from the desired output

3. **Recursive Search**: For each position in the target output, it tries all 8 possible 3-bit values (0-7), simulates the program until it produces output, and checks if it matches the expected value

4. **Simulation Optimization**: Instead of running the full program, it uses `simulate_until_output()` which runs only until the next output instruction, making the search much more efficient

The algorithm works because the program structure ensures that each 3-bit segment of register A influences a specific position in the output sequence, allowing for this divide-and-conquer approach.

## Improvements

The solution demonstrates excellent algorithmic thinking by avoiding brute force in favor of a structured search. The bit-by-bit construction approach reduces the search space from potentially billions of values to a manageable tree search.

### Algorithms

This problem showcases several important algorithmic concepts:
- **Computer Architecture Simulation**: Faithful implementation of a simple CPU
- **Reverse Engineering**: Working backwards from desired output to required input
- **Bit Manipulation**: Understanding how 3-bit segments affect program behavior
- **Recursive Search with Pruning**: Efficiently exploring the solution space

### Software Engineering

The `Computer` class is well-structured with clear separation of concerns:
- State management (registers, instruction pointer, output)
- Instruction implementation (each opcode as a separate method)
- Simulation control (run full program vs. run until output)
- Loop detection for infinite program detection

The code demonstrates good practices like input validation, state reset functionality, and clear method naming.

## Solutions

### Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:2400px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fpython%2Fday17.py&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>

### Agentic C++ translation of Python Solution

<div class="aside">
<iframe frameborder="0" scrolling="yes" style="width:100%; height:1972px;" allow="clipboard-write" src="https://emgithub.com/iframe.html?target=https%3A%2F%2Fgithub.com%2Folisheldon%2Faoc24%2Fblob%2Fmain%2Fagentic_ai_translations%2Fcpp%2Fday17.cpp&style=github-dark&type=code&showBorder=on&showLineNumbers=on&showCopy=on&fetchFromJsDelivr=on"></iframe>
</div>
