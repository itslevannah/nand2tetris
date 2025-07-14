---
layout: default
title: PC Chip
nav_order : 29
---

# PC Chip

### 1. PC Chip

The Program Counter (PC) is a 16-bit register with built-in control logic to support typical program counter operations: increment, load, and reset. It is used in the Hack computer to hold the address of the current instruction.

    If reset = 1, the counter is reset to 0.

    Else if load = 1, the counter is set to the input value.

    Else if inc = 1, the counter is incremented by 1.

    Otherwise, the counter holds its current value.


<img src="/nand2tetris/images/pc.png" width="500" height="200px"/>


### 2. Truth Table

| in (16-bit)         | load | inc | reset | out (16-bit)       | Notes                              |
|---------------------|------|-----|--------|---------------------|------------------------------------|
| x                   | 0    | 0   | 1      | 0000000000000000    | Reset to 0                         |
| 0000000000001010    | 1    | 0   | 0      | 0000000000001010    | Load 10                            |
| x                   | 0    | 1   | 0      | prev + 1            | Increment by 1                     |
| x                   | 0    | 0   | 0      | previous value      | Hold                               |
| 0000000000001111    | 1    | 1   | 0      | 0000000000001111    | Load overrides increment           |
| x                   | 1    | x   | 1      | 0000000000000000    | Reset overrides load and increment |


### 3. Implementation 


<img src="/nand2tetris/logisim/pc.png" width="500" height="200px"/>

### 4. Implementation (HDL)

The PC chip combines a Register, Inc16, and Mux16 chips to achieve its logic. Control signals are evaluated in the following priority: reset > load > inc.

```hdl
CHIP PC {
    IN in[16], load, inc, reset;
    OUT out[16];

    PARTS:
    // Calculate next value with proper priority: reset > load > inc
    Inc16(in=out, out=incOut);
    Mux16(a=out, b=incOut, sel=inc, out=incOrHold);
    Mux16(a=incOrHold, b=in, sel=load, out=loadOrInc);
    Mux16(a=loadOrInc, b=false, sel=reset, out=nextPC);

    // Register load signal: load if reset, load, or inc is active
    Or(a=reset, b=load, out=loadOrReset);
    Or(a=loadOrReset, b=inc, out=shouldLoad);
    Register(in=nextPC, load=shouldLoad, out=out);
}
 ```