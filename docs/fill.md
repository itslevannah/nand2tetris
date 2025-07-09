---
layout: default
title: Fill.asm Program
nav_order : 30
---

# Fill.asm Program 

### 1. Description

Fill.asm is a simple Hack assembly program that continuously fills or clears the screen based on the user's keyboard input:

    If any key is pressed, the screen is completely black (i.e., filled with 1s).

    If no key is pressed, the screen is completely white (i.e., filled with 0s).

It demonstrates keyboard input reading, screen memory manipulation, and use of loops and conditional jumps in Hack Assembly.


### 2. Pseudo Logic

```
Loop forever:
    If (key is pressed):
        Fill screen with black (all 1s)
    Else:
        Clear screen to white (all 0s)

```


### 3. Behavior Table

| Keyboard Input | Screen Action           | Description                              |
|----------------|--------------------------|------------------------------------------|
| 0              | Clear (write 0s)         | No key is pressed → blank screen         |
| >0             | Fill (write 1s)          | Key is pressed → filled (black) screen   |



### 4. Instruction Walkthrough

```
    // Initialize screen pointer
    @SCREEN
    D=A
    @addr
    M=D         // addr = SCREEN (16384)

    // Infinite loop
    (LOOP)
    // Check keyboard
    @KBD
    D=M

    // Jump to FILL if key pressed (D > 0)
    @FILL
    D;JGT

    // Otherwise, CLEAR
    (CLEAR)
        @SCREEN
        D=A
        @addr
        M=D       // Reset addr to SCREEN

        @8192
        D=A
        @count
        M=D       // count = 8192

        (CLEAR_LOOP)
            @addr
            A=M
            M=0    // Write 0 (white)

            @addr
            M=M+1  // addr++

            @count
            MD=M-1 // count--, D=count

            @CLEAR_LOOP
            D;JGT  // Loop if count > 0

        @LOOP
        0;JMP     // Return to main loop

    (FILL)
        @SCREEN
        D=A
        @addr
        M=D       // Reset addr to SCREEN

        @8192
        D=A
        @count
        M=D       // count = 8192

        (FILL_LOOP)
            @addr
            A=M
            M=-1   // Write -1 (black, all 1s)

            @addr
            M=M+1   // addr++

            @count
            MD=M-1  // count--, D=count

            @FILL_LOOP
            D;JGT   // Loop if count > 0

        @LOOP
        0;JMP      // Return to main loop
 ```
 ### 5. Memory Map Usage

| Symbol        | Address Range | Purpose                         |
| ------------- | ------------- | ------------------------------- |
| `SCREEN`      | 16384–24575   | Start of screen memory          |
| `KBD`         | 24576         | Memory-mapped keyboard register |
| `addr`        | Variable      | Current screen address          |
| `count`       | Variable      | Number of pixels left to write  |
| `screenStart` | Variable      | Holds start of screen memory    |


### 6. Test & Behavior in Simulator

To run Fill.asm in the CPU Emulator:

    Load the assembled version (Fill.hack).

    Run slowly or step through to see the screen being filled.

    Press any key — screen turns black.

    Release the key — screen turns white.
