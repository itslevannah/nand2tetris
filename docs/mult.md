---
layout: default
title: Mult.asm Program
nav_order : 31
---

# Mult.asm Program 

### 1. Description

Mult.asm is a Hack assembly program that multiplies two non-negative integers using repeated addition.

    It expects inputs R0 = x and R1 = y

    It computes R2 = x × y using a loop: adds x to a total y times

    Designed to run on the Hack computer, not on the CPU emulator alone (since it relies on RAM addresses)

This is a pure-software implementation of multiplication for a machine without a native multiply instruction.

### 2. Pseudo Logic

```
R2 = 0
repeat R1 times:
    R2 = R2 + R0

```


### 3. Behavior Table

| R0 (x) | R1 (y) | R2 (x × y) | Description                     |
|--------|--------|------------|---------------------------------|
| 3      | 4      | 12         | 3 added 4 times                 |
| 0      | 5      | 0          | Anything times 0 = 0            |
| 7      | 0      | 0          | 0 repetitions → 0               |
| 1      | 1      | 1          | 1 × 1 = 1                       |


### 4. Instruction Walkthrough

```
    // Load first number (multiplicand) into D
    @R0
    D=M            // D = R0

    // Store D into temp variable x
    @x
    M=D            // x = R0

    // Load second number (multiplier)
    @R1
    D=M            // D = R1

    // Store D into counter
    @count
    M=D            // count = R1

    // Initialize result = 0
    @R2
    M=0

    (LOOP)
        // If count == 0, we’re done
        @count
        D=M
        @END
        D;JEQ

        // Add x to R2 (R2 += x)
        @x
        D=M
        @R2
        M=M+D

        // Decrement count
        @count
        M=M-1

        // Repeat
        @LOOP
        0;JMP

    (END)
        // Done
        @END
        0;JMP

 ```

### 5. Instruction Walkthrough

| Symbol  | Meaning                   | Type     |
| ------- | ------------------------- | -------- |
| `R0`    | Multiplicand (x)          | Input    |
| `R1`    | Multiplier (y)            | Input    |
| `R2`    | Product (x × y)           | Output   |
| `x`     | Copy of R0                | Variable |
| `count` | Loop counter (copy of R1) | Variable |

### 6. Memory Map

| Address | Symbol   | Description             |
|---------|----------|-------------------------|
| 0       | R0       | First input (x)         |
| 1       | R1       | Second input (y)        |
| 2       | R2       | Output (x × y)          |
| 16      | x        | Copy of R0              |
| 17      | count    | Loop counter            |

### 7. Notes
    Program works for non-negative integers only

    It uses repeated addition — not optimized for speed

    Mult.asm demonstrates how to implement arithmetic operations in low-level Hack assembly using only basic instructions
