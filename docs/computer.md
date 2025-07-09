---
layout: default
title: Computer
nav_order : 34
---

# Computer 

### 1. Computer Chip

The Computer chip is the top-level architecture of the Hack platform. It integrates the CPU, Memory, and Program Counter (PC). It fetches instructions from the ROM (instruction memory), executes them via the CPU, and stores or retrieves data via the Memory chip.

The Computer chip supports:

    Instruction fetching

    Memory reads/writes

    Program flow control (jump, reset, halt, etc.)

<img src="/nand2tetris/images/computer.png" width="500" height="200px"/>


### 2. Truth Table

| ROM[instruction] | Memory[inM] | load | reset | Result                                |
|------------------|-------------|------|--------|----------------------------------------|
| C-instruction    | valid input | 1    | 0      | Performs ALU computation, stores result |
| A-instruction    | x           | 0    | 0      | Loads constant/address into A register  |
| x                | x           | x    | 1      | Resets the Program Counter to 0         |


### 3. Implementation (HDL)

The Computer chip connects:

    CPU

    Memory

    ROM32K (for instructions)

It routes the instruction into the CPU, the memory data into the CPU, and output signals from the CPU into Memory and the PC.


```hdl
CHIP Computer {
    IN reset;
    
    PARTS:
    // Instruction ROM (holds the program)
    ROM32K(address=pc, out=instruction);

    // Memory (RAM + Screen + Keyboard)
    Memory(in=outM, load=writeM, address=addressM, out=inM);

    // CPU (central processor)
    CPU(
        inM=inM,
        instruction=instruction,
        reset=reset,
        outM=outM,
        writeM=writeM,
        addressM=addressM,
        pc=pc
    );
}

 ```